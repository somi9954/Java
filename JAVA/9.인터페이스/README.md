# 인터페이스(interface)

## 인터페이스란?

- interface : 설계 목적의 용도로 한정된 클래스의 일종
- 추상 메서드와 상수만 정의한다.
- 구현되는것은  아무것도 없고 밑그림만 그려져 있는 ‘기본 설계도’라고 할 수있다.

인터페이스는 클래스를 작성하는것과 같다 class 대신 interface를 사용한다. 사용하는 방법은 다음과 같다.

```java
[접근제어자]interface 인터페이스명{
  ...
	접근제어자 abstact 메서드이름 (매개변수1, 매개변수2 ...)
  ...
}
```

```java
package section12;

public abstract class Phone {
	abstract void openingLogo(); 
	abstract void powerOn();     //공통 구현부가 사라짐
  abstract void powerOff();   //공통 구현부가 사라짐
  abstract void charge();     //새로운 메서드 추가 
}
```

interface에도 클래스처럼 접근제어자로 public 또는 default만 사용할 수 있다.

인터페이스에서는 필드 대신 상수를 선언할 수 있다. 단 상수이기 때문에 인터페이스는 고정된 값만 선언할 수 있다.

```java
[접근제어자]interface 인터페이스명{
	public static final 자료형 상수명 = 값;
  ...
}
```

```java
package section12;

public abstract class Phone {

	public static final int MAX_BATTERY_CAPACITY = 100;

	
	abstract void powerOn(); //공통구현부가 사라짐
  abstract void powerOff(); //공통 구현부가 사라짐
  abstract boolean isOn();     //새로운 메서드 추가 
	abstract void watchUttube(); //새로운 메서드 추가 
  abstract void charge();      //새로운 메서드 추가 
}
```

<aside>
💡 인터페이스의 멤버들은 다음과 같이 제약이 있다.
- 모든 멤버변수는 public static final이어야 하며, 이를 생략할 수 있다.
- 모든 메서드는 public abstract 이어야 하며, 이를 생략할 수 있다.
단, static메서드와 디폴트 메서드는 예외(JDK1.8부터)

</aside>

인텔리제이에서 패키지에서 생성시 새로만들기 ⇒ 자바클래스 ⇒ 인터페이스를 선택하여 만들수 있다.

![image](https://github.com/somi9954/Java/assets/137499604/237dad68-19e5-4be2-891c-5a2be2a9e246)


## 클래스에서 인터페이스 구현하기

하위 클래스가 구현을 통해서 객체 생성

인터페이스는 하위클래스가 추상메서드를 구현하는지를 가장 중점 사항
->implements(구현하다..)

여러개의 인터페이스를 하나의 클래스에서 구현 가능

인터페이스 구현과 형변환(다형성)

다형성은자식 클래스의 인스턴스를 조상타입의 참조변수로 참조하는것이 가능하다. 인터페이스 역시 이를 구현한 클래스의 조상이라 할 수 있으므로 해당 인터페이스 타입의 참조변수로 이를 구현한 클래스의 인스턴스를 참조할 수 있으며, 인터페이스 타입으로 형변환도 가능하다.

```java
package section12;

public class ThreeStarPhone implements Phone {
	int batteryCapacity = 35;
	boolean isOn = false;

	@Override
	public void powerOn() { // 구현하지 않으면 에러 발생
		if(batteryCapacity){
		System.out.println("★★★폰이 커졌습니다.★★★");
		isOn = true;
	} else { 
		System.out.println("배터리가 부족합니다.");
  }
	@Override
	public void powerOff() { // 구현하지 않으면 에러 발생
		System.out.println("★★★폰이 꺼졌습니다.★★★\n");
		isOn = false;
   }
	public boolean isOn() { // 구현하지 않으면 에러 발생
			if(isOn){
				return true;
		} else { 
		    return false;
	  }

		@Override
	public void watchUtube() { // 구현하지 않으면 에러 발생
		if(batteryCapacity > 15){
		System.out.println("--- U튜브 시청 중 ---");
		int batteryCapacity -= 10;
	 System.out.println("잔여 배터리..." + batteryCapacity + "%\n");
	} else { 
		System.out.println("배터리가 부족합니다.");
		powerOff();
  }
}

	@Override
	public void charge() { // 구현하지 않으면 에러 발생
		if(batteryCapacity < phone.MAX_BATTERY_CAPACITY - 20){
		System.out.println("--- 충전중 ---");
		 batteryCapacity += 10;
    System.out.println("잔여 배터리..." + batteryCapacity + "%\n");
	} else { 
		System.out.println("충전할 필요가ㅏ 없습니다.");
		 System.out.println("잔여 배터리..." + batteryCapacity + "%\n");
    }
  }
}

```

```java
package section12;

class Person {
	Phone p;

	Person (Phone p) { // 타입 변환을 통해 다형성을 구현할 수 있음
		this.p = p;
	}
	
	void buyNewPhone(Phone p) {
		this.p = p;
		System.out.println("= = = = = = = = = = = = = = = = = =");
		System.out.println("새 폰을 샀습니다!");
	}
	
	void turnOnPhone() {
		p.powerOn();
	}
	
	void turnOffPhone() {
		p.powerOff();
	}
	
	void watchUtube() {
		if(p.isOn()) {
			p.watchUtube();
		} else {
			System.out.println("폰이 꺼져 있기 때문에 U튜브를 볼 수 없습니다.");
		}
	}
 void chargePhone() {
		p.charge();
}
```

```java
package section12;

public class EX12_14 {
	public static void main(String[] args) {
		Person jimin = new Person(new PineapplePhone());
		jimin.turnOnPhone();
		for(int i = 1; i < 6; i++) {
			jimin.watchUtube();
			
			if(i % 3 == 0) {
				jimin.chargePhone();
			}
		}
		
		jimin.buyNewPhone(new ThreeStarPhone());
		jimin.turnOnPhone();
		
		for(int i = 1; i < 5; i++) {
			jimin.watchUtube();
			
			if(i % 3 == 0) {
				jimin.chargePhone();
			}
		}
	}
}
```

```java
출력값
@@@Power On!!@@@

---watching Utube ---
battery is... 30%

---watching Utube ---
battery is... 20%

---watching Utube ---
battery is... 10%

---charging ---
battery is... 15%

---watching Utube ---
battery is... 5%

Low battery...
@@@Power Off!!@@@

==================
새 폰을 샀습니다. 
★★★폰이 켜졌습니다.★★★

--- U튜브 시청 중---
잔여 배터리...25%

--- U튜브 시청 중---
잔여 배터리...15%

배터리가 부족합니다.
★★★폰이 꺼졌습니다.★★★

--- 충전 중 ---
잔여 배터리...25%

폰이 꺼져 있기 때문에 U튜브를 볼 수 없습니다.

```

<aside>
💡 인터페이스의  장점
- 실제 구현 클래스의 내용을 보지 않고도 개발 코드로 객체를 사용할 수 있다. ⇒ 정보 은닉
- 구현 클래스들이 독립적으로 구현되고 사용될 수 있다. 개발 코드에서 객체 변경이 필요할때, 개발 코드의 수정을 최소화할 수 있다.
⇒모듈화

</aside>

## 인터페이스의 요소 살펴보기

인터페이스 상수

- 클래스의 멤버 변수
- Static final 변수 ⇒ 상수 ⇒ 객체가 생성되면 접근할 수 있는 상수
⇒객체 생성과 상관없이 접근할수 있는 상수
- 선언된 모든 변수는 상수로 처리된다.

디폴트 메서드 → 자바 1.7 버전부터 사용가능해짐

- 완전히 구현된 메서드
- default
- 디폴트 메서드가 새로 추가 되어도 해당 인터페이스를 구현한 클래스를 변경하지 않아도 된다.
- 접근제한자는 public 이다.

정적 메서드

- static -> 인터페이스도 객체를 생성 할 필요 x, 접근 가능한 메서드
- 인스턴스를 사용하기 위해 클래스를 만들고 인스턴스를 생성하는 과정을 생략하고 바로 사용할 수 있게 구현해놓은 메서드입니다.

private 메서드

- JDK 11
- 인터페이스 내에서만 사용가능한 메서드이고 디폴트 메서드나 정적메서드에 사용하기 위해 작성되는 메서드 입니다. 인터페이스를 구현하는  클래스쪽에서 재정의하거나 사용할 수 없고 디폴트나 정적메서드를 통해서만 사용 가능합니다.

**defualt메서드와 static 메서드의 예는 다음과 같다.**

```java
class Ex7_11 {
	public static void main(String[] args) {
		Child3 c = new Child3();
		c.method1();
		c.method2();
		MyInterface.staticMethod(); 
		MyInterface2.staticMethod();
	}
}

class Child3 extends Parent3 implements MyInterface, MyInterface2 {
	public void method1() {	
		System.out.println("method1() in Child3"); // żŔšöśóŔĚľů
	}			
}

class Parent3 {
	public void method2() {	 
		System.out.println("method2() in Parent3");
	}
}

interface MyInterface {
	default void method1() {   // default 메서드
		System.out.println("method1() in MyInterface");
	}

	default void method2() {  // default 메서드
		System.out.println("method2() in MyInterface");
	}

	static void staticMethod() {  static 메서드
		System.out.println("staticMethod() in MyInterface");
	}
}

interface MyInterface2 {
	default void method1() {  // default 메서드
		System.out.println("method1() in MyInterface2");
	}

	static void staticMethod() {  //static 메서드
		System.out.println("staticMethod() in MyInterface2");
	}
}
```

```java
출력값
method1() in Child3
method2() in Parent3
staticMethod() in MyInterface
staticMethod() in MyInterface2
```

private 메서드를 사용하는 방법은 다음과 같다.

```java
public interface Programing {

    default void application(){
        debug(); // 내부에서만 사용 하여 구현 
    }
    private void debug(){                  // private 
        System.out.println("print");
    }

    public static void method() {
        call(); // 접근 가능 !
    }

    private static void call(){ // private static 메소드
        System.out.println("접근 가능");
    }
}
```

위의 예제 처럼 private void debug는 외부에서는 접근이 불가능하고 내부에서만 재사용 할수 있도록 사용된다.

private static으로 시작하는 메서드는 접근하고자 하는 메서드가 non-static이든, static이든 접근 가능하다.
static은 자원을 공유 하기 때문에 일반 인스턴스 변수, 메서드는 접근이 불가능하다. 따라서 private static을 사용함으로써 이러한 문제를 해결할 수 있게 되었다.

즉, 인터페이스 안에서 코드의 재사용과 캡슐화를 위해서 사용한다.

## 인터페이스 활용하기

1. 한 클래스가 여러 인터페이스를 구현하는 경우
- 인터페이스는 구현 코드가 없으므로 하나의 클래스가 여러 인터페이스를 구현 할 수 있습니다.
- 하지만 다른 인터페이스의 디폴트 메서드 이름이 중복되는 경우 에러가 발생하니 재정의해줄 필요가 있습니다.

```java
public interface Buy {
	
	void buy();
	
	default void order() {
		System.out.println("구매 주문");
	}

}
public interface Sell {
	
	void sell();
	
	default void order() {
		System.out.println("판매 주문");
	}
}
```

2개의 인터페이스를 각각 buy와 sell이란 이름으로 만들고 동일한 이름의 default 메서드 order를 만듭니다.

```java
public class Customer implements Buy, Sell {

	@Override
	public void sell() {
		System.out.println("customer sell");
		
	}

	@Override
	public void buy() {
		System.out.println("customer buy");
	}
	
	public void order() {
		System.out.println("customer order");
	}
    
	public void sayHello() {
		System.out.println("hello");
	}
}
```

- 구매와 판매를 동시에하는 고객을 구현하기 위해 Buy와 Sell 두 인터페스를 모두 implements 합니다.
- 각각의 인터페이스에 있던 sell()과 buy()를 구현하는데는 문제가 없지만 이름이 같았던 order()는 재정의가 필요하다고 에러메세지가 떠서 재정의를 해줍니다.
- 마지막으로 Customer에서만 사용할 수 있는 sayHello()를 추가하고 마칩니다.

```java
public class CustomerTest {

	public static void main(String[] args) {
		
		Customer customer = new Customer();
		customer.buy();
		customer.sell();
		customer.order();
		customer.sayHello();
		
		Buy buyer = customer;
		buyer.buy();
		buyer.order();
		
		Sell seller = customer;
		seller.sell();
		seller.order();
		
	}

}
//결과
customer buy
customer sell
customer order
hello
customer buy
customer order
customer sell
customer order
```

- 실행을 위해 Test클래스를 만들고 Customer 인스턴스를 생성해 buy(),sell(),order(),sayHello()메소드를 사용합니다.
- 각각 Buy와 Sell에 인스턴스를 생성해 사용한 결과 각각의 메서드가 실행한것을 확인 할 수 있습니다.
- 1개의 클래스만 상속이 가능한 것과는 다르게 인터페이스는 여러개도 구현이 가능하고 중복될 수 있는 default 메서드만 유의해서 사용하면 된다는것을 알 수 있습니다.
1. 두 인터페이스의 디폴트 메서드가 중복되는 경우
2. 인터페이스 상속하기
- 인터페이스로부터만 상속이 가능하며, 다중상속 즉 여러개의 인터페이스로부터 상속 받는 것이 가능하다.
- 하위클래스가 가상 메서드 테이블의 주소를 자기 자신의 값을 가지고 구현을 하기 때문에 상위 인터페이스가 중복이여도 코드가 없고 하위클래스상에서만 코드가 있기 때문에 다중 구현이 가능하다.

```java
package section12;

public interface Microphone {
	abstract void sing();
}
```

```java
package section12;

public interface Speaker {
	abstract void music();
}
```

```java
package section12;

public interface BluetoothMIC extends Microphone, Speaker {
	abstract void connect();
}
```

```java
package section12;

public class TJmic implements BluetoothMIC {
	@Override
	public void sing() { // Microphone 인터페이스의 추상 메서드
		System.out.println("마이크에 대고 노래를 부릅니다.");
	}
	
	@Override
	public void music() { // Speaker 인터페이스의 추상 메서드
		System.out.println("마이크에 장착된 스피커로 반주가 나옵니다.");
	}
	
	@Override
	public void connect() { // BluetoothMIC 인터페이스의 추상 메서드
		System.out.println("핸드폰과 블루투스 연결이 되었습니다.");
	}
}
```

```java
package section12;

public class EX12_23 {
	public static void main(String[] args) {
		System.out.println("---TJmic 객체---");
		TJmic tj = new TJmic();
		tj.connect();
		tj.music();
		tj.sing();
		
		System.out.println("\n---TJmic 객체를 BluetoothMIC로 타입 변환---");
		BluetoothMIC bm = tj;
		bm.connect();
		bm.music();
		bm.sing();
		
		System.out.println("\n---TJmic 객체를 Microphone으로 타입 변환---");
		Microphone m = tj;
		// m.connect(); ← 호출 불가능
		// m.music(); ← 호출 불가능
		m.sing();
		
		System.out.println("\n---TJmic 객체를 Speaker로 타입 변환---");
		Speaker s = tj;
		// s.connect(); ← 호출 불가능
		s.music();
		// s.sing(); ← 호출 불가능
	}
}
```

```java
출력
---TJmic객체---
핸드폰과 블루투스 연결이 되었습니다.
마이크에 장착된 스피커로 반주가 나옵니다.
마이크에 대고 노래를 부릅니다.

---TJmic객체를 BluetoothMIC로 타입 변환---
핸드폰과 블루투스 연결이 되었습니다.
마이크에 장착된 스피커로 반주가 나옵니다.
마이크에 대고 노래를 부릅니다.

---TJmic객체를 Microphone로 타입 변환---
마이크에 대고 노래를 부릅니다.

---TJmic객체를 Speaker로 타입 변환---
마이크에 장착된 스피커로 반주가 나옵니다.
```

1. 인터페이스 구현과 클래스 상속 함께 쓰기

인터페이스 구현과 클레스 상속을 함께 하는 경우에 대해서 예제를 통해서 알아보도록 하겠습니다. 아래의 관계도에서 BookSelf는 Shlef라는 클래스를 상속하고 Queue 인터페이스를 구현을 동시에 합니다.

```java
import java.util.ArrayList;

public class Shelf {

	protected ArrayList<String> shelf;
	
	public Shelf() {
		shelf = new ArrayList<String>();
	}
	
	public ArrayList<String> getShelf(){
		return shelf;
	}
	
	public int getCount() {
		return shelf.size(); 
	}
}
```

- 상위 클래스인 Shelf를 생성하고 ArrayList을 선언하여 입력한 책을 보관할 수 있게 합니다.
- Shelf 생성자 안에 ArrayList의 생성자를 두고 getShelf()와 getCount()메서드를 만듭니다. 복습으로 .size는 현재 배열안에 들어있는 값이 몇개인지 알려주는 메서드입니다.

```java
public interface Queue {
	
	void enQueue(String title);
	String deQueue();
	
	int getSize();
}
```

Queue인터페이스를 만들고 책을 넣을 수 있는 enQueue()와 뺄 수 있는 deQueue()메서드를 생성합니다.

```java
public class Bookshelf extends Shelf implements Queue {

	public void enQueue(String title) {
		shelf.add(title);
	}

	public String deQueue() {

		return shelf.remove(0);
	}

	public int getSize() {
		return getCount();
	}

}
```

BookShelf 클래스를 만들고 extends Shelf와 implements Queue를 동시에 적음으로 상속과 인터페이스 구현을 함께 합니다. enQueue()에 shelf.add(title)로 책을 축가하는 기능을 추가하고 deQueue()를 통해 .remove(0)사용함으로 배열에 첫번째 부터 지워주는 기능을 하게 합니다. 마지막으로 getSize()메서드를 통해 책장에 책이 얼마나 있는지 확인하는 기능을 추가합니다.

```java
public class BookshelfTest {

	public static void main(String[] args) {

		Queue bookQueue = new Bookshelf();
		bookQueue.enQueue("태백산맥1");
		bookQueue.enQueue("태백산맥2");
		bookQueue.enQueue("태백산맥3");
		
		System.out.println(bookQueue.deQueue());
		System.out.println(bookQueue.deQueue());
		System.out.println(bookQueue.deQueue());
	}

}

//출력값
태백산맥1
태백산맥2
태백산맥3
```

- Test클래스를 만들고 Bookshlf인스턴스를 생성하는데 Shelf로 해도되고 Queue로 해도 되지만 기능적인 면에서 Queue인터페이스를 타입으로하고 인스턴스를 생성합니다. 복습으로 Shlef 인스턴스를 생성 안해도
- ArrayLIst이 생성되는 이유는 BookShelf 생성이전에 상위 클랙스인 Shelf를 자동으로 생성하기 때문입니다. 이후 .enQueue 메서드로 책을 3권 추가하고 deQueue()메서드로 책을 한권씩 빼보면 배열에 앞에서부터 하나씩 빠지는걸 확인 할 수 있습니다.

## 실무에서 인터페이스를 사용하는 경우

- 인터페이스는 클래스가 제공할 기능을 선언하고 설계하는 것입니다.
- 만약 여러 클래스가 같은 메서드를 서로 다르게 구현한다면, 우선 인터페이스에 메서드를 선언한 다음 인터페이스를 구현한 각 클래스에서 같은 메서드에 대해 다양한 기능을 구현하면 됩니다.
- 이것이 바로 인터페이스를 이용한 다형성의 구현입니다.
- 인터페이스를 잘 정의하는 것이 확장성 있는 프로그램을 만드는 시작입니다.

## ****함수형 인터페이스(Functional Interface)****

- 추상 메소드를 딱 하나만 가지고 있는 인터페이스
(두 개의 메소드가 있다면 함수형 인터페이스가 아닙니다.)
- SAM(Single Abstract Method) 인터페이스
- @FunctionalInterface 애노테이션을 가지고 있는 인터페이스

```java
@FunctionalInterface
public interface RunSomething {
    void doIt();
		//void doItAgain(); 

		static void printName(){
        System.out.println("catsbi");
    }
    
    default void printAge(){
        System.out.println("33");
    }
}
```

⇒ 위 코드를 보면 printName()과 printAge 메소드도 있는데 함수형 인터페이스가 아닐까요? 답은 **함수형 인터페이스(Functional Interface)가 맞다** 입니다. 중요한건 static 메소드와 default메소드가 있는게아니라 **추상 메소드** 가 1개만 있어야 한다는 것입니다.

⇒@FunctionalInterface 함수형 인터페이스를 정의할일이 있을때는 인터페이스에 이 어노테이션을 붙혀주면 더 명시적으로 구분할 수 있고 함수형 인터페이스 규칙을 위반하면 컴파일시 에러가 발생하게 됩니다.

그렇다면 이 함수형 인터페이스를 어떻게 구현하여 사용할까요?

### ****기존의 방법****

: 익명 내부 클래스를 만들어 사용.

```java
public class Foo {
    public static void main(String[] args) {
        //익명 내부 클래스(anonymous inner class)
        RunSomething runSomething = new RunSomething() {
            @Override
            public void doIt() {...}
        };
    }
}
```

****자바 8 이후의 방법****

람다표현식(Lambda Expressions)을 이용하여 간략하게 구현

```java
public class Foo {
    public static void main(String[] args) {
        RunSomething runSomething = () -> System.out.println("Hello");
    }
}
```

만약 함수내에서 처리해야하는게 하나가 아니라면 아래와 같이 사용합니다.

```java
public class Foo {
    public static void main(String[] args) {
        RunSomething runSomething = () -> {
            System.out.println("Hello");
            System.out.println("two line");
        };
    }
}
```

### **자바에서 제공하는 함수형 인터페이스**

Java가 기본으로 제공하는 함수형 인터페이스

- [java.lang.funcation 패키지](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html) → 자바에서 미리 정의해둔 자주 사용할만한 함수 인터페이스
- Function
- BiFunction
- Consumer
- Supplier
- Predicate
- UnaryOperator
- BinaryOperator

**Function<T, R>**

- T 타입을 받아서 R 타입을 리턴하는 함수 인터페이스
    - R apply(T t)
- 함수 조합용 메소드
    - andThen
    - compose
    
    ```java
    FunctionalInterface
      public interface Function<T, R> {
        R apply(T t);
    
        default <V> Function<V, R> compose(Function<? super V, ? extends T> before) {
            Objects.requireNonNull(before);
            return (V v) -> apply(before.apply(v));
        }
    
        default <V> Function<T, V> andThen(Function<? super R, ? extends V> after) {
            Objects.requireNonNull(after);
            return (T t) -> after.apply(apply(t));
        }
    
        static <T> Function<T, T> identity() {
          return t -> t;
        }
      }
    ```
    
    - **compose:** before 메서드 실행 후 결과를 받아서 현재 메소드 실행. 제네릭 타입은 처음 input과 마지막 output의 타입이다. 즉 ,메서드를 순서대로 실행시키기 위한 함수
    - **andThen:** compose와 반대로 현재 메소드를 실행 후 매게 변수로 받은 람다를 실행
    - **identity:** 자신의 값을 그대로 리턴하는 스테틱 메서드
    
    **ompose , andThen 차이점**
    
    andThen()과 compose()의 차이점은 어떤 함수형 인터페이스부터 먼저 처리하느냐의 차이가 있다.
    
    ```css
    인터페이스A.compose(인터페이스B);
    B실행 -> A실행
    
    인터페이스A.andThen(인터페이스B);
    A실행 -> B실행
    ```
    
    **BiFunction<T,U,R>**
    
    - 두 개의 값(T, U)를 받아서 R 타입을 리턴하는 함수 인터페이스
        - R apply(T t, U u)
    - 함수 조합용 메소드
        - andThen
    
    ```java
    @FunctionalInterface
    public interface BiFunction<T, U, R> {
        R apply(T t, U u);
    
        default <V> BiFunction<T, U, V> andThen(Function<? super R, ? extends V> after) {
            Objects.requireNonNull(after);
            return (T t, U u) -> after.apply(apply(t, u));
        }
    }
    ```
    
    - **andThen:** 현재 메소드를 실행 후 매게 변수로 받은 람다를 실행
    
    **Consumer<T>**
    
    - T 타입을 받아서 아무값도 리턴하지 않는 함수 인터페이스
        - void Accept(T t)
    - 함수 조합용 메소드
        - andThen
    
    ```java
    @FunctionalInterface
      public interface Consumer<T> {
        void accept(T t);
    
         default Consumer<T> andThen(Consumer<? super T> after) {
            Objects.requireNonNull(after);
            return (T t) -> { accept(t); after.accept(t); };
        }
      }
    ```
    
    - **andThen:** Consumer 인터페이스는 처리 결과를 리턴하지 않기 때문에 andThen() 디폴트 메서드는 함수형 인터페이스의 호출 순서만을 정한다.
    
    **Supplier<T>**
    
    - T 타입의 값을 제공하는 함수 인터페이스
        - T get()
    
    ```java
    @FunctionalInterface
    public interface Supplier<T> {
      T get();
    }
    ```
    
    - **get:** 제네릭으로 전달받은 타입으로 값을 전달
    
    **Predicate<T>**
    
    - T 타입을 받아서 boolean을 리턴하는 함수 인터페이스
        - boolean test(T t)
    - 함수 조합용 메소드
        - And
        - Or
        - Negate
    
    ```java
    @FunctionalInterface
    public interface Predicate<T> {
      boolean test(T t);
    
      default Predicate<T> and(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> test(t) && other.test(t);
      }
    
      default Predicate<T> negate() {
        return (t) -> !test(t);
      }
    
      default Predicate<T> or(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> test(t) || other.test(t);
      }
    
      static <T> Predicate<T> isEqual(Object targetRef) {
        return (null == targetRef)
          ? Objects::isNull
            : object -> targetRef.equals(object);
      }
    }
    ```
    
    - **and:** 인자로 받는 다른 Predicate의 람다 수행 내용과 , 자기 자신의 람다 수행 내용을 &&연산
    - **or:** 인자로받는 다른 Predicate의 람다 수행내용과 , 자기자신의 람다 수행내용을 ||연산
    - **negate:** 람다 수행 내용을 ! 연산
    
    **UnaryOperator**
    
    - Function의 특수한 형태로, 입력값 하나를 받아서 동일한 타입을 리턴하는 함수인터페이스
    
    **BinaryOperator**
    
    - BiFunction의 특수한 형태로, 동일한 타입의 입렵값 두개를 받아 리턴하는 함수인터페이스
    
    컴파일러가 자동 추가해 주는 부분
    
    1. 기본 생성자
    2. 생성자의 첫번째 라인 → super()
    3. 인터페이스의 메서드 → public abstract
    4. 인터페이스의 정의된 변수 → public static final 정적 상수
    5. 참조 변수를 출력 → 변수.toString
