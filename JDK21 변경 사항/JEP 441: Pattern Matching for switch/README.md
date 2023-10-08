# JEP 441: Pattern Matching for switch 


* 앞선 JEP 440에서 살펴보았듯 자바는 최근 패턴 매칭 부분을 상당히 개선시키고 있는데, 이번에는 패턴 매칭을 스위치 문까지 확장시켰다.

#### Instanceof 사용
* 기존의 스위치 문은 특정 타입 여부를 검사하는 것이 상당히 제한적이였기 때문에, 특정 타입인지 검사하려면 instance of에 if-else 문법을 사용해야 했다.

```JAVA
// Prior to Java 21
static String formatter(Object obj) {
    String formatted = "unknown";
    if (obj instanceof Integer i) {
        formatted = String.format("int %d", i);
    } else if (obj instanceof Long l) {
        formatted = String.format("long %d", l);
    } else if (obj instanceof Double d) {
        formatted = String.format("double %f", d);
    } else if (obj instanceof String s) {
        formatted = String.format("String %s", s);
    }
    return formatted;
}
```

* 하지만 자바 21부터는 이러한 부분을 개선하였고, 다음과 같은 간결한 방식으로 패턴 매칭을 처리할 수 있게 되었다.

```JAVA
// As of Java 21
static String formatterPatternSwitch(Object obj) {
    return switch (obj) {
        case Integer i -> String.format("int %d", i);
        case Long l    -> String.format("long %d", l);
        case Double d  -> String.format("double %f", d);
        case String s  -> String.format("String %s", s);
        default        -> obj.toString();
    };
}
```

#### null 검사
* 기존에는 스위치 문의 파라미터가 null이라면 NPE(NullPointerException)을 던지기 때문에, null에 대한 검사가 스위치 문 외부에서 수행되어야 했다.

```JAVA
// Prior to Java 21
static void testFooBarOld(String s) {
    if (s == null) {
        System.out.println("Oops!");
        return;
    }
    switch (s) {
        case "Foo", "Bar" -> System.out.println("Great");
        default           -> System.out.println("Ok");
    }
}
```
* 하지만 자바21부터는 이러한 부분을 개선하였고, null에 해당하는 케이스를 스위치 내부에서 검사할 수 있게 되었다.
```JAVA
// As of Java 21
static void testFooBarNew(String s) {
    switch (s) {
        case null         -> System.out.println("Oops");
        case "Foo", "Bar" -> System.out.println("Great");
        default           -> System.out.println("Ok");
    }
}
```

### case 세분화
* case 문은 여러 값에 대한 검사를 필요로 하기 때문에 세분화될 수 있다. 자바 21 이전에는 이러한 부분을 코드로 작성하면 상당히 복잡한 구조로 만들 수 밖에 없었다.

```JAVA
// As of Java 21
static void testStringOld(String response) {
    switch (response) {
        case null -> { }
        case String s -> {
            if (s.equalsIgnoreCase("YES"))
                System.out.println("You got it");
            else if (s.equalsIgnoreCase("NO"))
                System.out.println("Shame");
            else
                System.out.println("Sorry?");
        }
    }
}
```

* 자바 21부터는 이러한 부분 역시 개선이 되었고, 다음과 같이 세분화할 수 있게 되었다. 이를 통해 보다 읽기 좋은 스위치 문 작성이 가능해진 것이다.

```JAVA
// As of Java 21
static void testStringNew(String response) {
    switch (response) {
        case null -> { }
        case String s
        when s.equalsIgnoreCase("YES") -> {
            System.out.println("You got it");
        }
        case String s
        when s.equalsIgnoreCase("NO") -> {
            System.out.println("Shame");
        }
        case String s -> {
            System.out.println("Sorry?");
        }
    }
}
```

 

### enum 개선
* 기존에는 스위치 문에서 enum을 사용하는 것이 상당히 제한적이였다.

```JAVA
// Prior to Java 21
public enum Suit { CLUBS, DIAMONDS, HEARTS, SPADES }

static void testforHearts(Suit s) {
    switch (s) {
        case HEARTS -> System.out.println("It's a heart!");
        default -> System.out.println("Some other suit");
    }
}
```

* 앞서 살펴본 새로운 문법인 case 세분화를 도입하여도, 코드는 불필요하게 장황해졌고, 복잡성이 완전히 해결되지 않았다.

```JAVA
// As of Java 21
sealed interface CardClassification permits Suit, Tarot {}
public enum Suit implements CardClassification { CLUBS, DIAMONDS, HEARTS, SPADES }
final class Tarot implements CardClassification {}

static void exhaustiveSwitchWithoutEnumSupport(CardClassification c) {
    switch (c) {
        case Suit s when s == Suit.CLUBS -> {
            System.out.println("It's clubs");
        }
        case Suit s when s == Suit.DIAMONDS -> {
            System.out.println("It's diamonds");
        }
        case Suit s when s == Suit.HEARTS -> {
            System.out.println("It's hearts");
        }
        case Suit s -> {
            System.out.println("It's spades");
        }
        case Tarot t -> {
            System.out.println("It's a tarot");
        }
    }
}
```
 
* 그래서 이러한 부분을 완전히 해결하고자 다음과 같은 문법으로 코드를 작성할 수 있도록 개선되었다. 이를 통해 더욱 가독성있는 enum 관련 스위치 문을 작성할 수 있을 것이다.

```JAVA
// As of Java 21
static void exhaustiveSwitchWithBetterEnumSupport(CardClassification c) {
    switch (c) {
        case Suit.CLUBS -> {
            System.out.println("It's clubs");
        }
        case Suit.DIAMONDS -> {
            System.out.println("It's diamonds");
        }
        case Suit.HEARTS -> {
            System.out.println("It's hearts");
        }
        case Suit.SPADES -> {
            System.out.println("It's spades");
        }
        case Tarot t -> {
            System.out.println("It's a tarot");
        }
    }
}
```
 ---- 
출처 : https://mangkyu.tistory.com/308 </br>
출처 : https://openjdk.org/jeps/441
