## 오버로딩 Overloading

같은 이름의 메서드를 지원하면서 매개변수의 ***유형***과 ***개수***가 다르도록 하는 기술

자바는 매개변수의 자료형 / 개수 / 순서를 기반으로 메서드를 구별하므로 하나의 클래스 안에서 같은 이름의 메서드를 여러 개 구현하고 필요에 따라 메서드를 선택해 사용할 수 있다.

오버로딩은 곧 **새로운 메서드를 정의** 하는것이다.

- 메서드(함수)의 시그니처

```html
패키지명 + 클래스명 + 반환값 타입 +함수명 + 매개변수 + 예외 전가
```

## 오버로딩 예제

```java
package section11;

class Parent {
	public void display() {
		System.out.println("부모 클래스의 display() 메서드입니다.");
	}
}
```

```java
class Child extends Parent {
	//오버로딩된 display() 메서드
	public void display(String str) {
		System.out.priln(str);
	}
}
```

```java
public class Inheritance06 {
	public static void main(String[] args) {
		Child ch = new Child();
	  ch.display("오버로딩된 display() 메서드입니다.");
	}
}
```

```java
출력값
오버로딩된 display() 메서드입니다.
```
