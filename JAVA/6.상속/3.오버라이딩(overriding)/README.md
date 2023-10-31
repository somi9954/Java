## 오버라이딩(overriding) : 재정의

:부모 클래스를 상속 받은 자식 클래스는 부모 클래스의 필드와 메서드를 가져와서 그대로 사용할 수 있다. 하지만 필요하다면 자식 클래스가 상속 받은 메서드의 내용을 변경해서 사용할 수도 있다. 이렇게 **상속 받은 메서드를 변경해서 다시 구현 하는것을 오버라이딩(Overriding)**이라고 한다. 

### 오버라이딩의 조건 및 방법

- 부모 클래스의 메서드 이름/반환 타입/ 매개변수와 동일해야 한다.
- 부모 클래스의 메서드 보다 접근 제한을 줄일 수 있으나(범위를 넓힐 수 있으나) 접근 제한을 늘릴 수는 없다.(범위를 좁힐 수 없다)
- @override 애노테이션을 사용한다.  메서드 오버라이딩을 구현하면 자동 완성으로 @override가 메서드 상단에 추가된다

      → ‘@’ 키워드를 애노테이션(annotation)이라고 부른다. 주석(comments)과 마찬가지로 코드를 생성하는데 직접적인 영향을 미치지 않고 정보 전달로만 쓰인다.

```java
public class Computer{
	void powerOn(){
		System.out.println("컴퓨터가 켜졌습니다.")
		}
	void powerOff(){
		System.out.println("컴퓨터가 꺼졌습니다.")
		}
```

```java
public class Samsong extends Computer{
	@override
	void powerOn(){
		System.out.println("아이 러브 삼송")
		}

```

```java
public class Overriding {
	public static void main(String[] args){
		Samsong samsong = new Samsong();
			samsong.powerOn();  //samsong 클래스에서 오버라이딩 된 메서드가 호출
			samsong.powerOff(); // computer 클래스의 메서드가 호출
		
		Computer computer = new computer();
			computer.powerOn();  //computer 클래스의 메서드가 호출
			computer.powerOff(); //computer 클래스의 메서드가 호출
```

```java
//출력값
아이 러브 삼송
컴퓨터가 꺼졌습니다.
컴퓨터가 켜졌습니다.
컴퓨터가 꺼졌습니다.
```

자식 클래스에서 오버라이딩 된 메서드는 자식 객체를 통해 호출하면 자식 클래스에서 구현한 메서드가 실행되고, 부모 객체를 통해 호출하면 자식 클래스와는 상관없이 부모 클래스의 원래 메서드로 호출 된다.

### 오버라이딩 super 키워

자식클래스에서 재정의 한것 과 부모 클래스에서 정의 되었던 것 모두 호출하려면 겹쳐 쓰는 방법이 있지만 super 키워드를 활용하면 중복을 줄일 수 있다.

super 키워드는 부모 클래스에서 상속 받은 필드나 메서드를 자식 클레스에서 참조하는 데 있어 사용하는 참조 변수이다.

this와 마찬가지로  super 참조 변수를 사용할 수 있는 대상도 인스턴스 메서드뿐이며, 클래스 메서드에서는 사용할 수 없다.

```java
public class Samsong extends Computer{
	@override
	void powerOn(){
		super.powerOn(); //부모 클래스의 powerOn() 메서드를 호출
		System.out.println("아이 러브 삼송")
		}

```

### 오버로딩(overloading) 과 오버라이딩(overriding)차이점

오버로딩 : **새로운 메서드를 정의** 하는 것이다.

오버라이딩 : **상속받은 기존의 메서드를 재정의** 하는것

```java
class Parent {

    void display() { System.out.println("부모 클래스의 display() 메소드입니다."); }

}

class Child extends Parent {

    // 오버라이딩된 display() 메소드

    void display() { System.out.println("자식 클래스의 display() 메소드입니다."); }

    void display(String str) { System.out.println(str); } // 오버로딩된 display() 메소드

}

 

public class Inheritance06 {

    public static void main(String[] args) {

        Child ch = new Child();

        ch.display();

        ch.display("오버로딩된 display() 메소드입니다.");

    }

}
```

```java
출력값
자식 클래스의 display() 메소드입니다.
오버로딩된 display() 메소드입니다.
```

![image](https://github.com/somi9954/Java/assets/137499604/6f9f5b07-f932-42dc-b794-a2e1a020bacb)


**가상 메서드 테이블**

- 각 클래스마다 메서드 테이블이 존재
- 오버라이딩(재정의)된 경우는 재정의 된 메서드의 주소를 가리킴
- 메서드 이름이 동일할 경우 주소값이 동일하다고 생각할 수 있지만, 컴파일 될 때 각 메서드별로 맵핑된 주소값이 다르기 때문에 재정의된 메서드의 경우 각각 다른 주소를 보유하고 있고, 재정의되지 않은 메서드의 경우 동일한 주소값을 지닌다.

![image](https://github.com/somi9954/Java/assets/137499604/443862cf-653d-419f-8698-58352542fc0a)


![image](https://github.com/somi9954/Java/assets/137499604/7150f603-5adb-4f9e-afe4-b4c9be6ae045)
