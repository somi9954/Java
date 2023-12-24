# 추상클래스

## 추상클래스란?

- 추상적 - 정해지지 않다의 뜻으로 추상클래스는 메서드의 구현체가 정해지지 않은 클래스이다.
- 구제적 - 확실하게 정해진 의미로  구체적 클래스는  메서드의 구현체가 정해진 클래스이다.
- 하나 이상의 추상 메서드를 포함하는 클래스를 말한다.
- 일반 클래스처럼 독립적으로 생성자를 호출해 객체를 생성할 수 없다.
- 자식 클래스의 생성자에서 super()를 통해 추상 클래스의 생성자를 호출하여 부모 객체를 생성한 후 자식 객체를 생성한다.

## 추상메서드

- 설계만 해놓고 실제 수행될 내용은 작성하지 않은 미완성 메서드
- 공통 기능
*하위클래스가 상속을 통해서 공통 기능을 공유, 설계대로 추상메서드를 정의 즉, 설계 원칙
-extends
- 추상클래스를 만드는 방법은  **abstract 키워드**를 사용하면 가능하다.
- {} (구현부) 대신 ;를 사용한다.
- 메서드의 선언부(declatration)만 봐도 어떤 일을 하는 메서드인지 알 수 있습니다. 함수의 선언부 즉, 반환 값, 함수 이름, 매개변수를 정의한다는 것은 곧 함수의 역할이 무엇인지, 어떻게 구현해야 하는지를 정의한다는 뜻힙니다.
- 따라서 함수 몸체를 구현하는 것보다 중요한 것은 함수 선언부를 작성하는 것입니다.
- 자바에서 사용하는 메서드 역시 마찬가지로 **메서드를 선언한다는 것은 메서드가 해야 할 일을 명시해 두는 것입니다.**

<aside>
💡 추상 메서드를 1개 이상 선언하면, 그 클래스는 추상 클래스로 선언되어야 한다.

</aside>

## 추상클래스의 문법

- 추상클래스는 항상 추상 메서드를 포함한다.
- 추상 메서드는 구현 코드가 없다.
- 추상클래스를 만드는 방법은  **abstract 키워드**를 사용하면 가능하다.
- {} (구현부) 대신 ;를 사용한다.

```java
/* 주석을 통해 어떤 긱능을 수행할 목적으로 작성하였는지 설명한다*/
[접근제한자]abstract 리턴타입 메서드이름();
```

```java
**abstract class player { //추상클래스
	abstract void play(int pos); //추상메서드
	abstract void stop();       //추상메서드
}

class AudioPlayer extends Player {
	abstract void play(int pos) {/* 내용 생략*/}  //추상메서드를 구현
	abstract void stop() {/* 내용 생략*/ }     //추상메서드를 구현
}
abstract class AbstractPlayer extends Player {
	void play(int pos){/* 내용 생략 */} //추상메서드를 구현
}**
```

추상클래스로부터 상속받는 자손클래스는 오버라이딩을 통해 조상인 추상클래스의 추상메서드를 모두 구현해줘야 한다. 만일 조상으로부터 상속받은 추상메서드 중 하나라도 구현하지 않는다면, 자손클래스 역시 추상클래스로 지정해주어야 한다.

## 추상클래스를 만드는 이유

추상클래스에 구현된 정의가 없다. 그러므로 상속받으면 구현체를 메서드 객체로써 만들어야 한다. 하위클래스를 상속하는 다른 하위클래스는 반드시 규칙(메서드)를 따라야 한다. 추상클래스는 독자적으로 객체를 만들수 없기 때문이다.

- 자식클래스 간의 공통적인 필드와 메서드 이름을 통일할 수 있다 ⇒ 다형성을 구현하기 위한 탄한 기반
- 반드시 구현해야 하는 메서드를 선언함으로써 공통 규격을 제공한다 ⇒ 개발 시간을 단축시키는 방법이기도 하며 객체를 변경해야 할 경우 큰 효율을 느낄 수 있다.

## 추상클래스 구현하기

```java
package Example;

public abstract class Animal {
    String name;
    int age;
    
    public Animal(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public void move() {System.out.println("이동한다");}
    public void eat() {System.out.println("먹는다");}
    public abstract void bark(); //짖는 소리는 동물마다 다르므로 추상메서드로 생성
}
```

```java
package Example;

public class Dog extends Animal{

    public Dog(String name, int age) {
        super(name, age);
    }
    
    @Override
    public void bark() { //메서드 오버라이딩
        System.out.println("멍멍!!");
    }; 
}
```

```java
package Example;

public class Cat extends Animal{
    public Cat(String name, int age) {
        super(name, age);
    }
    
    @Override
    public void bark() { //메서드 오버라이딩
        System.out.println("야옹~~");
    }; 
}
```

```java
package Example;

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog("강아지",3);
        Cat cat = new Cat("고양이",3);
        
        dog.move();
        dog.bark();
        
        cat.move();
        cat.bark();
    }
}
```

![image](https://github.com/somi9954/Java/assets/137499604/10f9bddd-26e5-4650-8fe8-dd646edf43a8)


## 추상클래스와 다형성

- 추상 클래스는 하위에 구현된 여러 클래스를 하나의 자료형(상위 클래스 자료형)으로 선언하거나 대입할 수 있습니다.
- 추상 클래스에 선언된 메서드를 호출하면 가상 메서드에 의해 각 클래스에 구현된 기능이 호출됩니다.
- 즉, 하나의 코드가 다양한 자료형을 대상으로 동작하는 다형성을 활용할 수 있습니다.

```java
package abstractClassTest;
import java.util.Scanner;

abstract class Shape {	//추상 클래스, 부모 클래스

	public abstract void draw();	//추상 메소드
}

//Shape 클래스를 상속받아 5가지 클래스를 만든다.

class Point extends Shape {

	@Override
	public void draw() {	//추상 메소드 구현
		System.out.println("점을 찍는다.");
	}
}

class Line extends Shape {

	@Override
	public void draw() {	//추상 메소드 구현
		System.out.println("선을 그린다.");
	}
}

class Circle extends Shape {

	@Override
	public void draw() {	//추상 메소드 구현
		System.out.println("원을 그린다.");
	}
}

class Rect extends Shape {
	
	@Override
	public void draw() {	//추상 메소드 구현
		System.out.println("사각형을 그린다.");
	}
}

class TriAngle extends Shape {

	@Override
	public void draw() {	//추상 메소드 구현
		System.out.println("삼각형을 그린다.");
	}
}

public class PolymorphismTest {	// 메인 클래스

	public static void main(String[] args) {
		//클래스 배열에 클래스들의 생성자 저장
		Shape[] shapes={new Point(),new Line(),new Circle(),new Rect(),new TriAngle()};
		Scanner sc = new Scanner(System.in);
		System.out.print("원하는 번호를 입력하세요 ");
		int menu = sc.nextInt();	// 입력받은 값을 menu에 저장
		shapes[menu-1].draw();	//shapes배열에 입력받은 값의 draw() 메소드 실행
		
	}
}
```

![image](https://github.com/somi9954/Java/assets/137499604/0df07662-7be9-4a5e-baf1-216da0cfa6a4)


![image](https://github.com/somi9954/Java/assets/137499604/c7e0cbb9-c934-42c4-b215-edc705eea5b4)
