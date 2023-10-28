### 접근제어자

: 클래스명, 멤버변수, 멤버 메서드들의 접근 권한을 지정한다.

| 접근자 | 표시 | 클래스 내부 | 패키지 | 상속받은 클래스 | 이외의 영역 |
| --- | --- | --- | --- | --- | --- |
| private | - | O | X | X | X |
| default(package) | ~ | O | O | X | X |
| protected | # | O | O | O | X |
| public | + | O | O | O | O |

public - 외부 패키지, 동일 패키지 모두 클래스 내부, 외부 접근 가능(import)

- 클래스 / 생성자 : 모든 패키지, 모든 클래스 어디서나 해당 클래스로 객체를 생성 할 수 있습니다.
- 멤버(필드, 생성자, 메서드) : 모든 패키지, 모든 클래스 어디서나 객체를 통해서 접근할 수 있습니다.

protected - 동일 패키지에서만 내부, 외부 접근 가능 (default와 동일) + 상속을 통하면 외부 패키지에 있는 클래스더라도 클래스 내부에서 접근 가능 (+private) (default + private)

- 클래스 / 생성자 : 같은 패키지의 클래스에서 생성자를 호출해 객체를 생성할 수 있습니다. 또한, 다른 패키지더라도 해당 클래스의 자식 클래스라면 생성자를 호출해 객체를 생성할 수 있습니다.
- 멤버(필드, 생성자, 메서드) : 같은 패키지의 클래스에서 접근 및 사용할 수 있으며, 해당 클래스의 자식 클래스라면 다른 패키지에서라도 사용할 수 있다.

default (접근제어자를 정의 X) 동일 패키지에서만 내부, 외부 접근 가능

- 클래스 / 생성자 : 같은 패키지 내에서 어디서나 호출이 가능하며, 객체를 생성할 수 있습니다.
- 멤버(필드, 생성자, 메서드) : 같은 패키지 내에서 제한 없이 접근이 가능합니다..

private - 클래스 내부에서만 접근이 가능

- 클래스 / 생성자 : 모든 패키지, 모든 클래스 어디서나 해당 클래스로 객체를 생성 할 수 있습니다.
- 멤버(필드, 생성자, 메서드) : 모든 패키지, 모든 클래스 어디서나 객체를 통해서 접근할 수 있습니다.

메서드 재정의 시 접근제어자의 범위 변경

(좁은쪽에서 넓은쪽으로 )

접근제어자 접근 범위가 넓은 쪽으로 나열 하면 다음과 같다.

public> protected > default > pirvate

### 접근제어자를 쓰는 이유

애플리케이션이 커진다는 것은,  그만큼 문제점이 생길 확률도 커진다는 말이 됩니다. 특히 **로직이 망가지는 첫 번째 원인은 사용자라고 할 수 있습니다.** 즉, **객체를 사용하는 입장에서 객체 내부적으로 사용하는 변수나 메소드에 접근함으로써 개발자가 의도하지 못한 오동작을 일으키기도 합니다.**

이러한 문제로부터 **객체의 로직을 보호하기 위해서**는 **멤버에 따라서 외부의 접근을 허용하거나 차단해야 할 필요**가 생깁니다.

마치 은행이 누구나 접근할 수 있는 창구와 관계자 외에는 출입이 엄격하게 통제되는 금고를 구분하고 있는 이유와 같습니다.

접근제어자를 사용하는 또 다른 이유는 **사용자에게 객체를 조작할 수 있는 수단만을 제공함으로써 결과적으로 객체의 사용에 집중할 수 있도록 돕기 위함**입니다.

즉, ***의도치 않은 실수를 줄이기 위함***과 ***정보 은닉의 목적***으로 사용할 수 있습니다.

**접근제어자는 다음과 같이 사용합니다.**

- **public 접근제어자의 예시**

```java
public class PublicA {
	public int a;
	
public PublicA(int a) {
	this.a = a;
}
public void printA(){
	System.out.println("PublicA 클래스의 printA() 메서드 입니다.")
  }
}
```

```java
import.PublicA; //다른 패키지의 클래스를 사용하기 위한 import

public class PublicB {
	 public static void main(String[] args) {
			PublicA a = new PublicA(10);
				a.print();
```

- **default 접근제어자의 예시**

```java
package section10.access1;

public class DefaultC {
	public int variableC;
}
```

```java
package section10.access1;

public class PublicA {
		DefaultC dc = new DefaultC(); //같은 패키지이기 때문에 객체 생성 가능
		void methodA() {
			dc.variableC = 20; //public 으로 선언된 필드도 객체를 통해 접근 간으.
	}
}
```

```java
package section10.access2;
import section10.access1.*; // access1패키지의 모든 클래스를 사용하기 위한 import

public class PublicB { // 클래스 선언
	public static void main(String[] args) {
		DefaultC c = new DefaultC() //에러 the type PublicA is not visible
		//c.variableC = 10;  필드가 public이더라도 객체를  생성하지 못하기 때문에 호출을 하지 못한다.
	}
}
```

- **protected 접근제어자의 예시**

```java
package section10.access1;

public class Parent {
	protected void accessProtected() {
		System.out.println("Protected 멤버에 접근하였습니다.");
	}
}
```

```java
package section10.access2;
import section10.access1.*;

public class Child extends Parent { // 클래스 선언
	void accessTest() {
		super.accessProtected(); // 이렇게 접근이 가능합니다.
		Parent p1 = new Parent();
		// p1.accessProtected( ); ← 자식 클래스더라도, 객체로 접근하는것은 불가능합니다.
		// 에러 : The method accessProtected( ) from the type Parent is not visible
	}
}
```

```java
package section10.access2;
import section10.access1.*;

public class NotChild { // 클래스 선언
	void accessTest() {
		Parent p2 = new Parent();
		// p2.accessProtected( ); 에러 :
		// T he method accessProtected( ) from the type Parent is not visible
	}
}
```

- **private 접근제어자의 예시**

```java
public class Student {
	int studentID;
	// studentName 변수를 private으로 선언 
	private String studentName; 
	int grade;
	String address;
}
```

```java
public class Student {
	int studentID;
	// studentName 변수를 private으로 선언 
	private String studentName; 
	int grade;
	String address;
}
```

```java
public class StudentTest {
	public static void main(String[] args) {
		Student studentLee = new Student();
		studentLee.studentName = "이상원"; // 오류발생
	}
}
```

- StudentTest.java파일에 오류가 발생합니다.
- studentName 변수의 접근 제어자가 public일 때는 외부 클래스인 StudentTest.java 클래스에서 이 변수에 접근할 수 있었지만, private으로 바뀌면서 외부 클래스의 접근이 허용되지 않기 때문입니다.
- 접근제어자 private 의 데이터를 주고 받으려고 하고자 하면 **캡슐화**를 이용하여 사용할 수 있다.
