# 다중상속(2차 상속)

다중상속은 객체지향 프로그래밍에서 하나의 클래스가 여러 개의 클래스로부터 상속을 받는 것을 의미합니다. 즉, 하나의 클래스가 다른 여러 클래스의 특징을 모두 가지고 있는 것입니다.

예를 들어, 아래와 같은 코드가 있다고 가정해봅시다.

```java
class A:
    def method_a(self):
        print("A 클래스의 메소드")

class B:
    def method_b(self):
        print("B 클래스의 메소드")

class C(A, B):
    pass

c_instance = C()
c_instance.method_a() # "A 클래스의 메소드" 출력
c_instance.method_b() # "B 클래스의 메소드" 출력

```

위 코드에서 클래스 C는 클래스 A와 클래스 B를 다중상속 받았습니다. 따라서 C 클래스의 인스턴스인 c_instance는 A 클래스의 메소드인 method_a()와 B 클래스의 메소드인 method_b()를 모두 사용할 수 있습니다.

하지만 다중상속은 코드의 복잡도를 증가시킬 수 있으며, 상속 관계가 복잡해질수록 코드의 가독성이 떨어지는 단점이 있습니다. 따라서 다중상속을 사용할 때에는 신중하게 고려해야 합니다.

다음과 같이 다중상속 중 2차 상속의 예를 들면 다음과 같이 된다.

```java
package section10;

public class Car {
	void ride() {
		System.out.println("달립니다.");
	}
}
```

```java
package section10;

public class Bus extends Car {
	int peopleNum; // 승객 수
	
	Bus(int peopleNum) {
		this.peopleNum = peopleNum; // 승객 수 초기화
	}
	
	void takePerson() {
		System.out.println("승객이 버스에 탔습니다.");
		peopleNum++;
		System.out.println("지금까지 탑승한 승객은 " + peopleNum + "명입니다.");
	}
}
```

```java
package section10;

public class SchoolBus extends Bus {
	SchoolBus(int peopleNum) {
		super(peopleNum); // Bus 클래스의 생성자 호출
	}
	
	@Override
	void takePerson() { // Bus 클래스의 takePerson( ) 오버라이딩
		super.takePerson(); // Bus 클래스의 takePerson( ) 메서드 호출
		System.out.println("학생들이 자리에 모두 착석하고 출발합니다.");
	}
	
	@Override
	void ride() { // Car 클래스의 ride( ) 오버라이딩
		System.out.println("시속 50km/h로 천천히 달립니다.");
	}
}
```

```java
package section10;

public class EX10_24 {
	public static void main(String[] args) {
		SchoolBus sb = new SchoolBus(10);
		sb.takePerson();
		sb.ride();
	}
}
```

```java
출력값
승객이 버스에 탔습니다.
지금까지 탑승한 승객은 11명 입니다. 
학생들이 자리에 모두 착석하고 출발합니다.
시속 50km/h로 천천히 달립니다.
```

**자바는 다중상속이 지원되지 않는 이유**

```java
package section10;

public class Car {
	void ride() {
		System.out.println("달립니다.");
	}
}
```

```java
package section10;

public class Bus extends Car {
	int peopleNum; // 승객 수
	
	Bus(int peopleNum) {
		this.peopleNum = peopleNum; // 승객 수 초기화
	}
	
	void takePerson() {
		System.out.println("승객이 버스에 탔습니다.");
		peopleNum++;
		System.out.println("지금까지 탑승한 승객은 " + peopleNum + "명입니다.");
	}
}
```

```java
package section10;

public class Bus2 extends Car {
	int peopleNum; // 승객 수
	
	Bus2(int peopleNum) {
		this.peopleNum = peopleNum; // 승객 수 초기화
	}
	
	void takePerson() {
		System.out.println("승객이 버스에 탔습니다.");
		peopleNum++;
		System.out.println("지금까지 탑승한 승객은 " + peopleNum + "명입니다.");
	}
}
```

```java
package section10;

public class SchoolBus extends Bus, Bus2 {
	SchoolBus(int peopleNum) {
		super(peopleNum); // Bus 클래스의 생성자 호출
	}
	
	@Override
	void takePerson() { // Bus 클래스의 takePerson( ) 오버라이딩
		super.takePerson(); // Bus 클래스의 takePerson( ) 메서드 호출
		System.out.println("학생들이 자리에 모두 착석하고 출발합니다.");
	}
	
	@Override
	void ride() { // Car 클래스의 ride( ) 오버라이딩
		System.out.println("시속 50km/h로 천천히 달립니다.");
	}
}
```

```java
package section10;

public class EX10_24 {
	public static void main(String[] args) {
		SchoolBus sb = new SchoolBus(10);
		sb.takePerson();
		sb.ride();
	}
}
```

다중상속을 지원하게 되면 하나의 클래스가 여러 상위 클래스를 상속 받을 수 있습니다. 이런 특징 때문에 문제가 발생되는데, 바로 **‘다이아몬드 문제’**입니다.

![image](https://github.com/somi9954/Java/assets/137499604/64565d1e-b1eb-4006-b262-2c67d0816b25)


위 클래스 다이어그램과 같은 상속 구조에서 발생되는 문제가 다이아몬드 문제입니다.  예를들어 Car이라는 클래스가 ride()라는 이름의 메소드를 가지고 있다고 가정해본다. 그리고 Bus와 Bus2에 각각 오버라이딩하여 구현하였다면 Bus와 Bus2를 모두 상속받은 SchoolBus 입장에서는 어떤 부모 클래스의 takePerson() 메서드를 사용해야 하는지 그것에 대한 충돌이 생기게 된다.

SchoolBus 클래스 입장에서는 같은 이름의 takePerson가 두개의 상위 클래스에 모두 정의되어 있기 때문에, 어떤 메소드를 실행해야 될지 알 수가 없습니다. (그리고 위의 코드는 당연히 컴파일 되지 않습니다.)

같은 객체지향 언어인 C++에서는 이런 문제가 있음에도 불구하고 개발자에게 일임하고, 자바는 내부적으로 구현이 불가하도록 막아두었습니다. (C나 C++은 좀 더 개발자들을 믿고 자유를 주는 반면에 JAVA는 개발 편의성을 생각하는 언어라는 사실을 이 점에서도 알 수 있습니다.)

다만 인터페이스에서는 다중상속이 가능하다. 왜냐하면 기능에 대한 선언만 해두면 되기 때문에 다이아몬드 상속이 되더라도 충돌할 여지는 없다. 그러므로 인터페이스 경우 다중상속을 통한 문제는 발생되지 않는다.

### **Default Method (자바 8)**

인터페이스는 기능에 대한 선언만 가능하기 때문에 , 실제 코드를 구현한 로직은 포함될 수 없다. 하지만 자바8에서 이러한 룰을 깨뜨리는 기능이 나오게 되었는데 Default Method이다. 메소드 선언 시 default를 명시하게 되면 인터페이스 내부에서도 로직이 포함된 메서드를 선언 할 수있다.

<aside>
💡 접근제어자에서 사용하는 default와 같은 키워드이지만, 접근제어자는 아무것도 명시하지 않는 접근제어자를 default라고 하며 인터페이스의 default Method는 ‘default.’라는 키워드를 명시해야 한다.

</aside>

default라는 키워드를 메소드에 명시하게 되면 인터페이스 내부라도 코드를 작성할 수 있다.

사실 인터페이스는 기능에 대한 구현보다는, 기능에 대한 '선언'에 초점을 맞추어서 사용 하는데, 디펄트 메소드는 왜 등장했을까요? 자바 기본서 '자바의 신'에서는 디펄트 메소드에 대한 존재 이유를 아래와 같이 설명했습니다.

> ...(중략) ... 바로 "하위 호환성"때문이다. 예를 들어 설명하자면, 여러분들이 만약 오픈 소스코드를 만들었다고 가정하자. 그 오픈소스가 엄청 유명해져서 전 세계 사람들이 다 사용하고 있는데, 인터페이스에 새로운 메소드를 만들어야 하는 상황이 발생했다. 자칫 잘못하면 내가 만든 오픈소스를 사용한 사람들은 전부 오류가 발생하고 수정을 해야 하는 일이 발생할 수도 있다. 이럴 때 사용하는 것이 바로 default 메소드다. (자바의 신 2권)
> 

기존에 존재하던 인터페이스를 이용하여서 구현된 클래스를 만들고 사용하고 있는데 인터페이스를 보완하는 과정에서 추가적으로 구현해야 할 혹은 필수적으로 존재해야 할 메소드가 있다면, 이미 이 인터페이스를 구현한 클래스와의 호환성이 떨어 지게 됩니다. 이러한 경우 default 메소드를 추가하게 된다면 하위 호환성은 유지되고 인터페이스의 보완을 진행 할 수 있습니다.

실제로 스프링 프레임 워크 버전 4에서 WebMvcConfigure라는 인터페이스를 구현한 클래스 WebMvcConfigurerAdapter를 사용하였지만 자바8에서 default 메소드가 등장하고 WebMvcConfigurerAdapter클래스는 더 이상 사용되지 않습니다.

```java
interface MyInterface { 
    default void printHello() {
    	System.out.println("Hello World"); 
        } 
} 

class MyClass implements MyInterface {} 

public class DefaultMethod { 
    public static void main(String[] args) { 
    	MyClass myClass = new MyClass(); 
        myClass.printHello(); //실행결과 Hello World 출력 
    } 
}
```

---

출처 : https://siyoon210.tistory.com/95

참고 도서 - 멘토씨리즈 자바(코리아 교육 그룹)
