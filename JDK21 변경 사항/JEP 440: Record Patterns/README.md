# JEP 440: Record Patterns 
* 레코드(Record)에 타입 패턴을 함께 적용하여 레코드의 값을 손쉽게 처리할 수 있도록 도와준다.
* 자바 16에서는 instance of 연산자에 타입 패턴을 적용하여 패턴 매칭을 개선시켰다. 타입 패턴 덕분에 instance of 하위 블록에서는 직접적으로 타입 캐스팅할 필요가 없어졌다.

```JAVA
// Prior to Java 16
if (obj instanceof String) {
    String s = (String)obj;
    ... use s ...
}

// As of Java 16
if (obj instanceof String s) {
    ... use s ...
}
```

* 이러한 바탕은 자바 언어가 보다 데이터 중심적인 프로그래밍 스타일로 나아가기 위함인데, 자바 21부터는 레코드 타입에 대해 보다 개선된 방법으로 사용 가능해질 예정이다.
* 기존에는 레코드 클래스에 instance of 연산자를 적용하면 다음과 같이 사용했었다.
```JAVA
record Point(int x, int y) {}

static void printSum(Object obj) {
    if (obj instanceof Point p) {
        int x = p.x();
        int y = p.y();
        System.out.println(x+y);
    }
}
```

* 하지만 자바 21부터는 다음과 같은 방식으로 사용 가능해진다. 이를 통해 obj가 Point의 인스턴스인지 여부를 테스트할 뿐만 아니라 개발자를 대신해 접근자 메소드를 호출하여 직접 변수들에 접근할 수 있게 된다. 이렇듯 새롭게 도입되는 레코드 패턴(Record Pattern)은 레코드 객체를 분해해주는 기능이라고 볼 수 있다.
```JAVA
// As of Java 21
static void printSum(Object obj) {
    if (obj instanceof Point(int x, int y)) {
        System.out.println(x+y);
    }
}
```
----
출처 : https://mangkyu.tistory.com/308 </br>
출처 : https://openjdk.org/jeps/440

 
