# 제네릭스(Generics)

> 지네릭스는 다양한 타입의 객체들을 다루는 메서드나 컬렉션 클래스에 컴파일 시의 타입 체크를 해주는 기능
> 
> 
> 다시 말해, 다룰 객체의 타입을 미리 명시해줌으로써 번거로운 형변환을 줄여준다.
> 
> 타입의 안정성 확보가 된다.
> 

- 하나의 예시를 들어보자.

```java
import java.util.ArrayList;

public class GenericsTest {
    public static void main(String[] args) {
        ArrayList list = new ArrayList();
        list.add(10);
        list.add(20);
        list.add("30");

        Integer i = (Integer)list.get(2);
    }
}
```

- 프로그래머는 **`ArrayList`** 타입 변수에 **`Integer`** 타입의 값들만 넣기를 원한다. 하지만 **`ArrayList`** 클래스는 내부적으로 **`Object`** 타입의 배열로 값들을 저장하기 때문에 모든 타입의 변수를 저장할 수 있다. 이 결과 프로그래머의 실수로 인해 **`String`** 타입의 값이 들어가게 됐지만, 컴파일은 하위 클래스 타입의 값을 저장하는 것은 문제가 없으므로 문제가 없는 것 처럼 보인다.

- 하지만 코드를 실행하면 아래와 같은 **형변환 예외**가 발생한다.

***java.lang.ClassCastException**: class java.lang.String cannot be cast to class java.lang.Integer (java.lang.String and java.lang.Integer are in module java.base of loader 'bootstrap')*

- `list.get(2)`로 꺼내진 값은 `String`타입의 `“30”`이다. 이를 `Integer`타입으로 형변환을 하려 했기 때문에 런타임 에러가 발생한 것이다. 하지만 컴파일은 참조 변수가 **`Object`** 타입이기 때문에 이를 **`Integer`** 타입으로 형변환 하는 것은 문제가 없다고 판단해 버린다.

- **`Object`** 타입은 모든 클래스들의 상위 클래스기 때문에 보통 컴파일 시 문제가 되지 않는다. 안에 어떤 값이 담겨있는지 컴파일은 알 수가 없다. 따라서 위와 같이 프로그래머가 의도치 않게 다른 값을 넣어도 컴파일 시 에러가 발생하지 않고 실행 시 에러가 발생해 프로그램이 죽는 치명적 결함이 된다.

- 자바는 1.5 버전 이후부터 지네릭스를 도입해 위와 같은 문제를 해결하려 했다. 즉 실행 시 발생할 수 있는 에러를 컴파일로 가져와 프로그래머가 알아차리게 한 후, 수정할 수 있게하기 위함이다.

### 지네릭스의 용어

- Box<T>  : 지네릭 클래스
- T : 타입 매개변수, 클래스 내부에서 식별자 기호 T 를 클래스 필드와, 메소드의 매개변수의 타입으로 지정되어 있다.
- Box : 원시타입

```java
T - Type  여러개 쓰일 경우 T, U, R 
E - Element element를 뜻한다
K - Key key를 의미한다.
V - Value value를 의미하고 K와 많이 쓰인다. (예. Map)
N - Number
```

- 지네릭 타입은 클래스와 메서드에 선언할 수 있다.

```java
class Box<T>  { // 지네릭 타입 T를 선언. T는 타입변수
  T item;
  
   void setItem(T item)  {
     this.item = item;
  }
  
  T getItem() {
    return item;
  }
}
```

- 지네릭 클래스가 된 Box 클래스의 객체를 생성할 때는

- 다음과 같이 참조변수와 생성자에 타입 T대신 사용될 실제 타입을 지정해야 한다.

```java
Box<String> b = **new** Box<String>();  // 타입 T대신 실제 타입 지정
b.setItem(**new** Object());  // 에러. String 외의 타입은 지정 불가
b.setItem("ABC"); // OK. String 타입이므로 가능
```

- 예를 들어, Box과 Box는 지네릭 클래스 Box에 서로 다른 타입을 대입하여 호출한 것일 뿐, 서로 다른 클래스를 의미하지 않는다.
- 컴파일 후에 Box과 Box는 이들의 원시타입인 Box로 바뀐다. 즉, 지네릭타입이 제거된다.

```java
→ Object 클래스 → 객체가 생성될때 타입 매개변수의 자료형으로 변환
```

- 지네릭이 무엇인지 확인할 수 있는건 객체가 만들어지는 시점에  확인할 수 있다.

## **2. 지네릭스 제한**

<img src="https://github.com/somi9954/Java/assets/137499604/efc46c77-3259-44d5-86c6-19f773334c20" width="450">

- 모든 객체에 대해 동일하게 동작해야하는 static멤버에 타입변수 T를 사용할 수 없다.
    
- T는 인스턴스 변수로 간주되기 때문이다. (static 멤버는 인스턴스 변수를 참조할 수 없다.)
    
- 추가적으로 static 메서드의 매개변수로도 타입 매개 변수가 올 수 없다.

- static 멤버는 모든 객체가 하나의 static 멤버를 동일하게 공유하기 때문이다.
    
- 타입 변수를 사용함으로써 객체마다 다른 객체를 저장할 수 있게 하는 것이 지네릭의 핵심이다.
    
- T는 String이 될 수도 Integer가 될 수도 있는 것이다
    
- 그런데 Static이면 객체가 생성되기도 전에 이미 자료 타입이 정해져있어야 한다.
    
- 만약 static이 타입 변수을 가질 수 있다면 다른 자료타입을 가진 객체들이 충돌해버린다.
    
- 그렇기 때문에 Static 멤버들은 지네릭 타입 변수를 사용할 수 없는 것이다.
    
 <img src="https://github.com/somi9954/Java/assets/137499604/a4d6aa79-bdf7-443f-8907-c3239f1388e5" width="400">

    
- 지네릭 배열 타입의 참조변수를 선언하는 것은 가능하지만,
    
-  `new T[10]` 과 같이 배열을 생성하는 것은 안된다.
    
- new 연산자 때문인데, 이 연산자는 컴파일 시점에 타입 T가 무엇인지 정확히 알아야 한다. → new 연산자 뒤에 올 자료형은 자료 타입이 확정되어야 사용할 수 있다.
    
- instanceof 연산자도 같은 이유로 T를 피연산자로 사용할 수 없다.
    

## **3. 지네릭 클래스의 객체 생성과 사용**

- Apple이 Furuit의 자손이라고 가정해도

```java
Box<Fruit> appleBox = new Box<Apple>(); // 에러. 대입된 타입이 다르다.
```

- 단, 두 지네릭 클래스의 타입이 상속관계에 있고, 대입된 타입이 같은 것은 괜찮다.

```java
Box<Apple> appleBox = new FruitBox<Apple>();  // OK. 다형성
```

- 생성된 Box의 객체에 ‘void add(T item)‘으로 객체를 추가할 때, 대입된 타입과 다른 타입의 객체는 추가할 수 없다.

```java
Box<Apple> appleBox = new Box<Apple>();
appleBox.add(new Apple());  // OK.
appleBox.add(new Grape());  // 에러. Box<Apple>에는 Apple 객체와 Apple의 자손만 추가 가능
```

## **4. 제한된 지네릭 클래스**

- 지네릭 타입에 `extends`를 사용하면, 특정 타입의 자손들만 대입할 수 있게 제한할 수 있다.

```java
 class FruitBox<T extends Fruit> { //Fruit의 자손만 타입으로 지정 가능
  ArrayList<T> list = new ArrayList<T>();
  ...
}
```

- 인터페이스도 구현이 가능하다.

```jsx
<<T extends 타입1 & 타입2> -> T는 타입1의 하위 클래스 이고 타입2 인터페이스의 구현 클래스
```

- 인터페이스를 구현해야 한다는 제약이 필요하다면, 이때도 implements 대신 `extends`를 사용한다.

```java
 interface Eatable {}
  class FruitBox<T extends Eatable> {
  ...
}
```

- 클래스 Fruit의 자손이면서 Eatable 인터페이스도 구현해야하면 `&` 기호로 연결한다.

```java
class FruitBox <T extends  Fruit & Eatable> {
  ...
}`
```

## **5. 와일드 카드**

- 지네릭 타입은 컴파일러가 컴파일할 때만 사용하고 제거해버린다.

- 때문에 지네릭 타입이 다른 것만으로는 Overloading이 성립하지 않고 ‘메서드 중복 정의’가 된다.

- 이럴 때 사용하는 것이 와일드 카드이며, 와일드 카드는 어떤 타입도 될 수 있다. 기호 `?`로 표현한다.

- `?`만으로는 Object타입과 다를 게 없으므로, `extends`와 `super`로 상한과 하한을 제한할 수 있다.

```java
<? extends T> T와 그 하위들만 가능
<? super T> T와 그 상위들만  가능 -> Object도 포함
<?> 모든 타입 가능. <? extends Object>와 동일
```

- 와일드 카드에는 `&`을 사용할 수 없다.

<img src="https://github.com/somi9954/Java/assets/137499604/8e89ec88-ebae-46df-8267-ddd6c92d90c1" width="450">


- 예를 들어 Apple와 Grape가 있는데 각각 Fruit를 상속 받고 있다.

```java
Juicier 클래스에서 
public static void make(Basket < ? extends Fruit> basket){
	List<? items = basket.getItems();
	System.out.println(items);
}

(Basket < ? extends Fruit> basket) -> Fruit 포함한 Apple클래스와 Grape 클래스를 사용할 수 있다.
만약 (Basket < ? super Fruit> basket)  -> Fruit과 전 클래스를 상속하는 Object 클래스만 사용할 수 있다.
```

## **6. 지네릭 메소드**

> 메소드의 선언부에 지네릭 타입이 선언된 메소드가 지네릭 메소드다.
> 
> 
> 지네릭 메소드는 지네릭 클래스가 아닌 클래스에도 정의할 수 있다.
> 

```java
  class FruitBox<T> {
    ...
    static <T> void sort(List<T> list, Comparator<? super T> c) {
    ...
  }
}
```

- 지네릭 클래스에 정의된 타입 매개변수와 지네릭 메소드에 정의된 타입 매개변수는 전혀 별개의 것이다.
- static 멤버에는 타입 매개변수를 사용할 수 없지만, 이처럼 메소드에 지네릭 타입을 선언하고 사용하는 것은 가능하다.
    - 메소드에 선언된 지네릭 타입은 지역 변수를 선언한 것과 같다고 생각하면 이해하기 쉽다.
    - 타입 매개변수는 메소드 내에서만 지역적으로 사용될 것이므로 메소드가 static이건 아니건 상관없다.
    - 같은 이유로, 내부 클래스에 선언된 타입 문자가 외부 클래스의 타입 문자와 같아도 구별될 수 있다.
    
    [확인해보기](https://inpa.tistory.com/entry/JAVA-%E2%98%95-%EC%A0%9C%EB%84%A4%EB%A6%ADGenerics-%EA%B0%9C%EB%85%90-%EB%AC%B8%EB%B2%95-%EC%A0%95%EB%B3%B5%ED%95%98%EA%B8%B0#%ED%83%80%EC%9E%85_%ED%8C%8C%EB%9D%BC%EB%AF%B8%ED%84%B0_%EC%A0%95%EC%9D%98)
