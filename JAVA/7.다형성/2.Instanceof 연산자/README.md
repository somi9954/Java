## **Instanceof 연산자**

: 부모 클래스 타입으로 타입이 변환되어 저장된 변수는 안에 어떤 객체가 담겨 있는지 직접 확인해보지 않는 이상 내부 객체를 알기가 쉽지 않다. 오버라이딩 된 메서드가 있다면 확인이 가능하겠지만 만약 부모 클래스를 같이 상속 받고 있는 다른 클래스, 또는 부모 클래스와 구별할 수 있는 특정 멤버가 없을때 instanceof 연산자를 사용한다.

즉 참조 변수의 형 변환이 가능한지의 여부를 boolean의 타입으로 확인 할 수 있는 자바의 문법 요소이다.

= 업캐스팅, 다운 캐스팅 확인 검사!

선언하는 방법은 다음과 같습니다.

```java
객체 instanceof 타입(클래스명);
```

instanceof 연산자의 특징은 다음과 같다.

- instanceof 기준으로 왼쪽 객체가 생성될 때 오른쪽 타입으로 생성 되었는지 확인하는 연산자이다.
- 맞으면 true, 아니면 false를  반환하며 만약 null 가리키고 있으면 false를 반환한다.

### instanceof 연산자 예시

```java
package section11;

class Animal { }
class Pig extends Animal { }
class Cow extends Animal { }

class Farm {
	void sound(Animal animal) {
		if(animal instanceof Pig) { // animal 변수에 담긴 객체의 타입이 Pig이면,
			System.out.println("꿀꿀");
		} else { // animal 변수에 담긴 객체의 타입이 Pig가 아니면,
			System.out.println("음메");
		}
	}
}

public class EX11_15 {
	public static void main(String[] args) {
		Farm f = new Farm();
		Pig p = new Pig();
		Cow c = new Cow();
		f.sound(p);
		f.sound(c);
	}
}
```

```java
출력값 
꿀꿀 
음
```

### 다형성의 활용

카페에서 커피를 주문하는 것을 예로 Coffee 클래스에는 가격 정보를 담고 있다.

Coffee 클래스를 상속받는 Amercano 클래스와 CaffeLatte 클래스가 존재한다.

손님은 5만 원을 가지고 있다고 가정한다.

```java
class Coffee {
    int price;

    public Coffee(int price) {
        this.price = price;
    }
}

class Americano extends Coffee {
    public Americano() {
        super(4000); // 상위 메서드 생성자 호출
    }
    // Object 클래스 toString() 메서드 오버라이딩
    public String toString() { 
        return "아메리카노";
    }
}

class CaffeLatte extends Coffee {
    public CaffeLatte() {
        super(5000);
    }
    // Object 클래스 toString() 메서드 오버라이딩
    public String toString() {
        return "카페라떼";
    }
}

class Customer {
    int money = 50000;

    // 커피 구매 메서드(다형성 활용)
    void buyCoffee(Coffee coffee) {
        if (money < coffee.price) {
            System.out.println("잔액이 부족합니다.");
            return;
        }
        money -= coffee.price;
        System.out.println(coffee + "를 구매하였습니다.");
    }

    /* 아메리카노, 카페라떼 구매 메서드를 따로 구현하지 않아도 됨
    void buyCoffee(Americano americano) {
        money -= americano.price;
    }

    void buyCoffee(CaffeLatte caffeLatte) {
        money -= caffeLatte.price;
    } */
}
```

```java
public class PolymorphismEx {
    public static void main(String[] args) {
        Customer me = new Customer();
        me.buyCoffee(new Americano());
        me.buyCoffee(new CaffeLatte());

        System.out.println("현재 잔액: " + me.money);
    }
}
```

다음과 같이 다형성을 활용하여 개별 적인 커피의 구매 메서드를 따로 구현하지 않고, 상위 클래스인 Coffee의 자료형을 매개변수로 전달받으면, 하위 클래스 타입의 참조 변수는 매개변수로 전달될 수 있다.

이로써 반복적인 코드를 줄일 수 있다
