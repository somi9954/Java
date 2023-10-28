# 추상화(**abstraction)**

## 추상화의 의미

자바에서 추상화란, **여러 개체들의 공통적인 특징을 파악하여, 이를 하나의 개념으로 다루는 것**을 말합니다. 이를 통해 복잡한 현실 세계를 단순하고 이해하기 쉬운 모습으로 모델링할 수 있습니다.

즉, 객체의 공통적인 속성과 기능을 추출하여 정의하는것이다.

예를 들어, 동물이라는 개념을 추상화해보면, 동물이 가지는 공통적인 특징으로는 먹이를 먹고, 숨쉬고, 움직인다는 것이 있습니다. 이러한 특징들을 추출하여, Animal(동물)이라는 추상적인 개념을 만들어 낼 수 있습니다.

자바에서는 이러한 추상화 개념을 **인터페이스와 추상 클래스를 통해 구현**할 수 있습니다. 

**예를 들어**, 동물이라는 추상적인 개념을 인터페이스로 구현하면 다음과 같습니다.

```java
public interface Animal {
    public void eat(); 
    public void breathe();
    public void move();
}

```

또한, 이 인터페이스를 구현한 구체적인 클래스를 만들어, 실제 객체를 생성할 수 있습니다. 예를 들어, 개라는 동물을 구현한 클래스는 다음과 같습니다.

```java
public class Dog implements Animal {
    public void eat() {
        System.out.println("개가 먹이를 먹습니다.");
    }
    public void breathe() {
        System.out.println("개가 숨을 쉽니다.");
    }
    public void move() {
        System.out.println("개가 뛰어다닙니다.");
    }
}

```

이렇게 구현된 클래스를 사용하여, 다음과 같이 객체를 생성하고 사용할 수 있습니다.

```java
Animal myPet = new Dog();
myPet.eat(); // 개가 먹이를 먹습니다.
myPet.breathe(); // 개가 숨을 쉽니다.
myPet.move(); // 개가 뛰어다닙니다.

```

즉, 자바에서 추상화는 객체 지향 프로그래밍의 핵심 개념 중 하나로, 복잡한 문제를 간단하고 이해하기 쉬운 개념으로 단순화하는 것입니다.

추상화를 사용하는 이유는 추상화를 통해 잘 설계 됐다면 여러개의 클래스를 정의했을때 중복 코드가 현저히 줄어들 것이다.  코드가 간결해지기 때문에 생산성 증가, 가독성 증가, 에러 감소, 유지 보수시 시간 단축이 된다.

```java
// 일반 클래스
class Parent1 {
	void test() {}
}

// 일반 클래스를 상속받은 일반 클래스
class Child1 extends Parent1{}

// 추상 클래스
abstract class Parent2 { 
	
	abstract void test1();
	abstract void test2();
	abstract void test3();
	abstract void test4();
	abstract void test5();
	abstract void test6();
	abstract void test7();
	
	void test99() { 
		System.out.println("일반 메서드");
	}
	
}

// 추상클래스를 상속받은 일반 클래스
class Child2 extends Parent2 {

	@Override
	void test1() {

	}

	@Override
	void test2() {

	}

	@Override
	void test3() {

	}

	@Override
	void test4() {

	}

	@Override
	void test5() {

	}

	@Override
	void test6() {

	}

	@Override
	void test7() {
		
	}
	
}

// 추상클래스를 상속받은 일반클래스
class Child3 extends Parent2{

	@Override
	void test1() {
		
	}

	@Override
	void test2() {
		
	}

	@Override
	void test3() {
		
	}

	@Override
	void test4() {
		
	}

	@Override
	void test5() {
		
	}

	@Override
	void test6() {
		
	}

	@Override
	void test7() {
		
	}
	
}

public class OOPEx05 {

	public static void main(String[] args) {
	
	}

}
```
