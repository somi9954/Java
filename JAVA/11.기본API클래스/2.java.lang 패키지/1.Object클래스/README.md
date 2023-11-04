# Object 클래스

- Object 클래스는 **자바의 최상위 클래스**이다.
- 모든 클래스는 생성할 때 상속하지 않아도 Object를 자동으로 상속 받게 된다. 상속받는 extends를 사용하지 않아도 Object 클래스의 상속을 의미하는 **extends Object가 컴파일 과정에서 자동으로 쓰입니다.**
- 클래스를 생성하면 가지고 있는 여러 메서드를 그대로 사용하거나 override하여 사용할 수 있게 된다.

![image](https://github.com/somi9954/Java/assets/137499604/50ce1ba8-e89b-49d6-8d0d-73f84d2c0260)


String 클래스 JavaDoc 예시

![image](https://github.com/somi9954/Java/assets/137499604/76978568-dc83-4a4e-9aac-be8f55841418)

- **java.lang.Object** : 최상위 클래스
- java.lang.String : JavaDoc에서 검색한 클래스
- JavaDoc을 보니 String 클래스 역시 Object 클래스를 상속받았음을 알 수 있습니다.
- 모든 클래스가 **Object 클래스를 상속**받았으므로 **Object의 메서드를 사용할 수 있고, 재정의 할 수도 있고, Object형으로 변환할 수 도 있습니다.**
- 자바로 프로그래밍을 하다 보면 클래스가 Object형으로 변환되는 경우도 있고, Object에서 원래 클래스형으로 다운 캐스팅되는 경우도 있습니다.
- Object 클래스는 멤버변수는 없고 오직 11개의 메서드를 가지고 있다.

![image](https://github.com/somi9954/Java/assets/137499604/8034c77d-e28a-4d7f-b01a-d594ea95fbc3)


java API 문서에서의 Object 클래스

### Object 클래스에 정의된 메서드

| 메서드 | 설명 |
| --- | --- |
| String toString() | 객체를 문자열로 표현하여 반환합니다. 재정의하여 객체에 대한 설명이나 특정 멤버 변수 값을 반환합니다. |
| boolean equals(Object obj) | 두 인스턴스가 동일한지 여부를 반환합니다. 재정의하여 논리적으로 동일한 인스턴스임을 정의할 수 있습니다. |
| int hashCode() | 객체의 해시 코드 값을 반환합니다. |
| Object clone() | 객체를 복제하여 동일한 멤버 변수 값을 가진 새로운 인스턴스를 생성합니다. |
| Class getClass() | 객체의 Class 클래스를 반환합니다. |
| void finalize() | 인스턴스가 힙 메모리에서 제거될 때 가비지 컬렉터(GC)에 의해 호출되는 메서드입니다. 네트워크 연결 해제, 열려 있는 파일 스트림 해제 등을 구현합니다. |
| void wait() | 멀티스레드 프로그램에서 사용하는 메서드입니다. 쓰레드를 기다리는 상태(non runnable)로 만듭니다. |
| void notify() | wait() 메서드에 의해 기다리고 있는 쓰레드(non runnable 상태)를 실행 가능한 상태(runnable)로 가져옵니다. |
- Object 메서드 중에는 재정의 할 수 있는 메서드도 있고 그렇지 않은 메서드도 있습니다.
- Object 메서드 중에서 final 예약어로 선언된 메서드는 자바 쓰레드에서 사용하거나 클래스를 로딩하는 등 자바 가상 머신과 관련된 메서드이기 때문에 재정의할 수 없습니다.|

![image](https://github.com/somi9954/Java/assets/137499604/83c94bd9-71e4-4284-aabc-966ebc235793)


Object 클래스 메서드 이미지

### 객체 문자 정보 toString() 메서드

- Object 클래스에서 기본으로 제공하는 toString() 메서드는 이름 처럼 객체 정보를 문자열(String)로 바꾸어 준다.
- Object 클래스를 상속받은 모든 클래스는 toString()을 재정의할 수 있습니다.
- 재정의를 통해서 멤버변수의 값을 출력하는 값으로 많이 활용한다.
- 클래스를 작성할 때, toString()을 오버라이딩 하지 않으면 아래와 같은 내용이 그대로 사용 될것이다.

```java
getClass().getName() + '@' + Integer.toHexString(hashCode())
```

- toString()을 호출하면 클래스의 이름과 16진수의 해시코드를 얻을 수 있다

<aside>
💡 참고)
Class getClass() : 클래스의 정보가 담겨 있는 객체를 반환
getName() : 클래스 이름 (전체 클래스명 - 패키지명을 포함한 클래스명

</aside>

**String과 Integer클래스의 toString() 메서드**

```java
String str = new String("test"); 
System.out.println(str); // test 출력됨
~~Integer i1 = new Integer(100);~~
~~System.out.println(i1); // 100 출력됨~~

```

- 두 클래스의 출력 결과는 **클래스이름@해시코드 값**이 아니라 문자열 값 test, 정수값 100이 각각 출력됩니다.
- 그 이유는 String과 Integer 클래스는 toString() 메서드를 미리 재정의해 두었기 때문입니다.
- JDK에서 제공하는 클래스 중에는 toString() 메서드를 미리 재정의한 클래스가 많습니다.
- toString() 메서드가 재정의된 클래스는 '클래스의 이름@해시코드 값'을 출력하는 toString() 메서드의 원형이 아닌 **재정의된 메서드**가 호출되는 것입니다.

```java
package day11.object;

class Book {
	int bookNumber;
	String bookTitle;
	
	Book(int bookNumber, String bookTitle) {
		this.bookNumber = bookNumber;
		this.bookTitle = bookTitle;
	}
	
	@Override
	public String toString() { // toString() 메서드 재정의
		return bookTitle + "," + bookNumber;
	}
}

public class ToStringEx {
	public static void main(String[] args) {
		Book book1 = new Book(200, "개미");
		
		 // 클래스 정보(클래스 이름, 주소 값)
		System.out.println(book1);
		
		// toString())) 메서드로 인스턴스 정보(클래스 이름, 주소 값)를 보여 줌
		System.out.println(book1.toString());
	}
}

실행결과

개미,200
개미,200
```

toString**() 메서드 직접 재정의 하기**

```java
class Card2 {
	String kind;
	int number;

	Card2() {
		this("SPADE", 1);  // Card(String kind, int number)¸¦ È£Ãâ
	}

	Card2(String kind, int number) {
		this.kind = kind;
		this.number = number;
	}

	public String toString() {
		return "kind : " + kind + ", number : " + number;
	}
}

class Ex9_5 {
	public static void main(String[] args) {
		Card2 c1 = new Card2();
		Card2 c2 = new Card2("HEART", 10);
		System.out.println(c1.toString());
		System.out.println(c2.toString());
	}
}

실행 결과
kind: spade, number : 1
kind: heart, number : 10
```

- 조상클래스에 정의된 메서드를 자손클래스에서 메서드 재정의를 할 때 조상클래스의 접근 범위보다 같거나 더 넓어야 하기 때문에 Object 클래스에 정의된 toString()의 접근 제어자가 public 이므로 Card2 클래스의 toString()의 접근제어자도 public으로 정의 되었다.

### 객체 비교 equals() 메서드

- 기본 데이터들의 동등 비교를 위해 ‘==’비교 연산자를 사용한다. 하지만 객체에서의 의미는 조금  다르다. 객체를 동등 비교를 할 경우 해당 객체의 값을 비교하는 것이 아니라, 객체가 메모리에 있는 위치를 비교하게 된다. 따라서 참조형 데이터의 비교 연산에는 적절치 못하므로 객체의 데이터를 비교할때는 재정의를 하여 논리적으로 같은 인스턴스인지 확인하도록 구현할수 있는 equals()메서드를 사용한다.
- 매개변수로 객체의 참조변수를 받아서 비교하여 그 결과를  boolean 값(true/false)으로 알려주는 역할을 한다..
- 물리적 동일성(인스턴스 메모리 주소가 같음)뿐 아니라 **논리적 동일성(논리적으로 두 인스턴스가 같음)을 구현할 때도 equals() 메서드를 재정의**하여 사용합니다.

<aside>
💡 1) 동일성 비교
== : 동일성 비교 / 동일한 객체 / 동일한 주소인지 확인

2) 동등성 비교 : 가치가 같은 객체인지
Object equals를 재정의를 통해서 동등성 비교로 구현

</aside>

**Object 클래스의 equals() 메서드**

- 두 인스턴스가 물리적으로 같다는 것은, 두 인스턴스의 주소 값이 같은 경우를 말합니다. 즉, 두 변수가 같은 메모리 주소를 가리키고 있다는 뜻 입니다.

```java
Student studentLee = new Student(100, "이상원");
Student studentLee2 = studentLee; // 주소 복사

```

![image](https://github.com/somi9954/Java/assets/137499604/60ba841d-dfea-4104-8e55-d9b2d8bac8df)


- 두 변수는 다음 그림과 같이 동일한 인스턴스를 가리킵니다. 이 때 equals()메서드를 이용해 두 변수를 비교하면 동일하다는 결과가 나옵니다.
    
   ![image](https://github.com/somi9954/Java/assets/137499604/9ad32917-c527-4beb-a28f-fe650d090f8a)

    

```java
Student studentLee = new Student(100, "이상원");
Student studentLee2 = studentLee;
Student studentSang = new Student(100, "이상원");

```

![image](https://github.com/somi9954/Java/assets/137499604/3ea7f55d-4d1c-4bcf-a658-aa4bdb4b06a4)


- 위 코드를 표현한 그림은 다음과 같습니다.

![image](https://github.com/somi9954/Java/assets/137499604/669629a2-1bff-4aad-8792-05fe1ced2a74)


- studentLee, studentLee2가 가리키는 인스턴스와 studentSang이 가리키는 인스턴스는 서로 다른 주소를 가지고 있지만, 저장된 학생의 정보는 같습니다. 이런 경우 논리적으로는 studentLee, studentLee2와 studentSang을 같은 학생으로 처리하는 것이 맞을 것 입니다.

다음의 equals() 메서드의 예는 다음과 같다.

```java
package day11.object;

class Student{
	
	int studentId;
	String studentName;
	
	public Student(int studentId, String studentName){
		this.studentId = studentId;
		this.studentName = studentName;
	}
	
	public String toString(){
		return studentId + "," + studentName;
	}
}

public class EqualsTest {

	public static void main(String[] args) {

		Student studentLee = new Student(100, "이상원");
		Student studentLee2 = studentLee; // 주소 복사 
		Student studentSang = new Student(100, "이상원");

		// 동일한 주소의 두 인스턴스 비교 
		if(studentLee == studentLee2) // == 기호로 비교 
			System.out.println("studentLee와 studentLee2의 주소는 같습니다.");
		else
			System.out.println("studentLee와 studentLee2의 주소는 다릅니다.");
		
		if(studentLee.equals(studentLee2)) // equals() 메서드로 비교 
			System.out.println("studentLee와 studentLee2는 동일합니다.");
		else
			System.out.println("studentLee와 studentLee2는 동일하지 않습니다.");
		
		
		// 동일인이지만 인스턴스의 주소가 다른 경우 
		if(studentLee == studentSang) // == 기호로 비교 
			System.out.println("studentLee와 studentSang의 주소는 같습니다.");
		else
			System.out.println("studentLee와 studentSang의 주소는 다릅니다.");
		
		if(studentLee.equals(studentSang)) // equals() 메서드로 비교ㅕ
			System.out.println("studentLee와 studentSang은 동일합니다.");
		else
			System.out.println("studentLee와 studentSang은 동일하지 않습니다.");  
	
	}
}
```

![image](https://github.com/somi9954/Java/assets/137499604/db7a6afe-b45a-47f7-874e-c9d53398c19c)


- Object의 equals() 메서드의 원래 기능은 두 인스턴스의 주소를 비교하는 것입니다. 따라서 같은 주소인 경우만 equals() 메서드의 결과가 true가 됩니다.
- 두 인스턴스가 있을 때 ==는 단순히 물리적으로 같은 메모리 주소인지 여부를 확인할 수 있고, Object의 equals() 메서드는 재정의를 하여 논리적으로 같은 인스턴스인지(메모리 주소가 다르더라도 같은 학생인지) 확인하도록 구현할 수 있습니다.

**equals() 메서드 직접 재정의 하기**

```java
class Person {
	long id;

	public boolean equals(Object obj) {
		if(obj instanceof Person)
			return id ==((Person)obj).id;
		else
			return false;
	}

	Person(long id) {
		this.id = id;
	}
}

class Ex9_2 {
	public static void main(String[] args) {
		Person p1 = new Person(8011081111222L);
		Person p2 = new Person(8011081111222L);

		if(p1.equals(p2))
			System.out.println("p1과 p2는 같은 사람입니다.");
		else
			System.out.println("p1과 p2는 다른 사람입니다.");
	}
}

```

- equals() 메서드를 재정의하였습니다.
- equals() 메서드의 매개변수는 Object형 입니다. 비교될 객체가 Object형으로 전달되면 instanceof를 사용하여 매개변수의 원래 자료형이 Person인지 확인합니다.
- this의 id과 매개변수로 전달된 객체의 id가 같으면 true를 반환합니다.
- equals() 메서드를 재정의한 후 출력 결과를 보면 id가 같으므로 equals()는 true를 반환합니다.

**String과 Integer 클래스의 equals() 메서드**

- JDK에서 제공하는 String 클래스와 Integer 클래스에는 equals() 메서드가 이미 재정의 되어 있습니다.

```java
package day11.object;

public class StringEquals {
	public static void main(String[] args) {

		String str1 = new String("abc");
		String str2 = new String("abc");

		System.out.println(str1 == str2);  // 두 스트링 인스턴스의 주소 값은 다름
		System.out.println(str1.equals(str2)); // String 클래스의 equals 메소드가 재정의 됨

		Integer i1 = new Integer(100); // Integer 보다는 Integer.valueOf 사용 -> 인스턴스 주소는 같은 값에 대해 동일
		Integer i2 = new Integer(100);

		System.out.println(i1 == i2);   // 두 정수 인스턴스의 주소 값은 다름
		System.out.println(i1.equals(i2)); // Integer 클래스의 equals 메소드가 재정의 됨
	}
}
```

![image](https://github.com/somi9954/Java/assets/137499604/f743d0ff-5613-4cbc-a2e5-d663a61b3f51)


- 코드의 내용을 보면 str1과 str2는 서로 다른 인스턴스를 가리키기 때문에 str1 == str2의 결과는 false 입니다. 하지만 String 클래스의 equals() 메서드는 같은 문자열의 경우 true를, 그렇지 않은 경우 false를 반환하도록 **재정의**되어 있습니다.
- 두 문자열은 "abc"로 같은 값을 가지므로 str1.equals(str2)의 반환 값은 true입니다.
- Integer 클래스의 경우도 정수 값이 같은 경우 true를 반환하도록 equals() 메서드가 재정의되어 있습니다.

### 객체 해시코드 hashCode() 메서드

- 해시(hash)는 다량의 데이터를 저장하고 검색하는데 유용한 자료구조이다.
- 정보를 어디에 저장할 것인지, 어디서 가져올 것인지 해시 함수를 사용해서 구현한다.
- 해시 함수는 객체의 특정 정보(키 값)를 매개변수 값으로 넣으면 그 객체가 저장되어야 할 위치나 저장된 해시 테이블 주소(위치)를 반환한다.
- hashCode() 메서드 ⇒ 객체의 주소값
- 동등한 객체이면 일반적으로 hashcode도 같게 정의한다. 따라서 논리적으로 같은 두 객체도 같은 해시 코드 값을 반환하도록 hashCode() 메서드를 재정의해야 합니다. 다시 말해, equals() 메서드를 재정의 했다면 hashCode() 메서드도 재정의해야 합니다.
- • 자바에서는 인스턴스를 힙 메모리에 생성하여 관리할 해시 알고리즘을 사용합니다.

**String과 Integer 클래스의 hashCode() 메서드**

- String 클래스와 Integer 클래스의 equals() 메서드는 재정의되어 있습니다. 마찬가지로 hashCode() 메서드도 함께 재정의되어 있습니다.

```java
package day11.object;

public class HashCodeTest {
	public static void main(String[] args) {

		String str1 = new String("abc");
		String str2 = new String("abc");

		// abc 문자열의 해시 코드 값 출력
		System.out.println(str1.hashCode());
		System.out.println(str2.hashCode());

		~~Integer i1 = new Integer(100);~~
		~~Integer i2 = new Integer(100);~~

		// Integer(100)의 해시코드 값 출력
		System.out.println(i1.hashCode());
		System.out.println(i2.hashCode());
	}
}

실행결과

96354
96354
100
100

```

- String 클래스는 같은 문자열을 가진 경우 즉, equals() 메서드의 결과 같이 true인 경우 hashCode() 메서드는 동일한 해시 코드 값을 반환합니다.
- Integer 클래스의 hashCode() 메서드는 정수 값을 반환하도록 재정의되어 있습니다.

**day11/object/EqualsTest.java - Student 클래스에서 hashCode()메서드 재정의**

```java
package day11.object;

class Student{
	...
	@Override
	public int hashCode() {
		return studentId;
	}
}

public class EqualsTest {
	public static void main(String[] args) {
		...
		System.out.println("studentLee의 hashCode :" +studentLee.hashCode());
		System.out.println("studentSang의 hashCode :" +studentSang.hashCode());

		System.out.println("studentLee의 실제 주소값 :"+ System.identityHashCode(studentLee));
		System.out.println("studentSang의 실제 주소값 :"+ System.identityHashCode(studentSang));
	}
}

실행결과

studentLee와 studentLee2의 주소는 같습니다.
studentLee와 studentLee2는 동일합니다.
studentLee와 studentSang의 주소는 다릅니다.
studentLee와 studentSang은 동일합니다.
studentLee의 hashCode :100
studentSang의 hashCode :100
studentLee의 실제 주소값 :1586600255
studentSang의 실제 주소값 :474675244

```

- 출력 결과를 보면 studentLee, studentSang은 학번이 같기 때문에 논리적으로 같은지 확인하는 equals() 메서드 출력 값이 true 입니다.
- 또한 같은 해시 코드 값을 반환하고 있습니다.
- hashCode() 메서드를 재정의했을 때 실제 인스턴스 주소 값은 System.indentityHashCode() 메서드를 사용하면 알 수 있습니다. studentLee와 studentSang은 실제 메모리 주소 값은 다릅니다. 즉, 논리적으로는 같지만 실제로는 다른 인스턴스 입니다.

- 동등성의 기준 equals 와  hashcode를 꼭 사용하여야 한다.
