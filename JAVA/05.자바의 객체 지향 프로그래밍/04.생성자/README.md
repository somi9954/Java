# 생성자란? - 객체를 만드는 기능

- 클래스를 구성하는 구성요소 중 하나인 생성자는 객체를 생성할 때 호출되어 객체의 초기화를 담당하는 특별한 메서드이다. 객체를 생성하고 초기화 하기 위해서는 반드시 생성자를 호출해야 한다. 따라서 객체를 생성해야 하는 라이브러리용 클래스는 모두 생성자를 가지고 있다.
- 생성자 역시 메서드처럼 클래스 내에서 선언되며, 구조도 메서드와 유사하지만 리턴값이 없다는점이 다르다. 그렇다고 생성자 앞에 리턴값이 없음을 뜻하는 키워드 void 를 사용하지는 않고 아무것도 적지 않는다.
- 일반 메서드과는 다르게 생성자는 호출할 수 있는 곳이 정해져 있다. 생성자는 클래스를 기반으로 객체를 생성할 때 객체의 초기화를 담당하는 역할을 하므로 객체를 생성할 때만 사용할 수 있다.

참고) **데이터 영역 메모리(코드 & 상수 영역 메모리)**

클래스 로더 -> 구조화 → classs class 객체 생성(클래스 정보 확인 파일) -> 데이터 영역 로드

**생성자의 조건**

1. 생성자의 이름은 클래스의 이름과 같아야 한다.
2. 생성자는 리턴 값이 없다.

<aside>
💡 생성자도 메서드이기 때문에 리턴갑이 없다는 의미의 void를 붙여야 하지만, 모든 생성자가 리턴값이 없으므로 void를 생략할 수 있게 한것이다.

</aside>

생성자의 기본 구조는 다음과 같다.

```jsx
클래스명(매개변수1, 매개변수2, ...) {
// 인스턴스 생성시 수행할 코드,
// 주로 인스턴스 변수의 초기화 코드를 적는다.
}
```

생성자를 호출할 때는 다음과 같다.

```java
클래스명 객체명 = new 클래스명();
                 이 메서드가 바로 생성자이다.!
```

생성자는 다음의 예와 같다.

```java
public class Student {
    int id; //학번
    String name; //이름
    String subject; //전공과목

void study(){
        System.out.println(name + "이 " +  subject +  "를 공부한다.");

    }
}
```

```java
public class Ex01 {
    public static void main(String[] args) {
        Student s1 = new Student();
        s1.id= 1000;
        s1.name = "학생1";
        s1.subject = "과목1";

        s1.study();
  }
}
```

```java
출력값
학생1이 과목1를 공부한다.
```

**기본생성자** (디폴트 생성자)

: 자바의 모든 클래스에서는 하나 이상의 생성자가 정의되어 있어야 한다. 클래스를 생성하면서 개발자가 직접 생성자를 선언하지 않았지만, 자바 컴파일러가 기본 생성자를 자동으로 제공한다.  컴파일 할 때, 소스파일(*.java)의 클래스에 생성자가 하나도 정의되지 않은 경우 컴파이러는 자동적으로 아래와 같은 내용의 기본 생성자를 추가하여 컴파일 한다.

```java
클래스 이름() {} //기본 생성자 -> 주소값이 들어있는 생성자
Point() { } // Point클래스의 기본 생성자 
```

특별하게 인스턴스 초기화 작업이 요구되어지지 않는다면 생성자를 정의하지 않고 컴파일러가 제공하는 기본 생성자를 사용하는것도 좋다.

<aside>
💡 클래스의 ‘접근제어자(Access Modifier)’가 public 인경우에는 기본 생성자로 ‘public 클래스이름 (){}’ 이 추가 된다.

</aside>

**매개변수가 있는 생성자 (매개변수 2개)**

- 매개변수는 일반 메서드와 마찬가지로 생략할 수 있으며, 2개 이상 전달할 수도 있다.

다음과 같이 생성이 가능하다.

```java
public class Person {
String name;
int age;

Person(String name, int age) {
	name = name;
	age = a;
   }

void introduce() {
	System.out.println( "안녕하세요. 저는 " + age + "세 " + name + "입니다. " );
  }
}
```

```java
public class Ex {
	public static void main(String[] args) {
		Person p1 = new Person("김자바", 20);
		Person p2 = new Person("이코딩", 40);

    p1.introduce;
		p2.introduce;
   }
}

출력값 
안녕하세요. 저는 20세 김자바입니다.
안녕하세요. 저는 40세 이코딩입니다.
```

**생성자 오버로딩**

[오버로딩(overloading)](https://www.notion.so/overloading-680a17c4e8da48bc8f5f0ef4e7787a48?pvs=21) 

```java
public class Book {
	String title = "제목없음";
	int series = 1;
	int page = 100;
	
	Book() { // ← 생성자 1
		
	}
	
	Book(String t) { // ← 생성자 2
		title = t;
	}
	
	Book(String t, int p) { // ← 생성자 3
		title = t;
		page = p;	
	}
	
	Book(int s, String t) { // ← 생성자 4
		series = s;
		title = t;
	}
}
}
```

```java
public class EX09_12 {
	public static void main(String[] args) {
		Book b1 = new Book(); // ← 생성자 1
		System.out.println("b1.title : " + b1.title);
		System.out.println("b1.series : " + b1.series);
		System.out.println("b1.page : " + b1.page);
		
		Book b2 = new Book("멘토시리즈 자바"); // ← 생성자 2
		System.out.println("b2.title : " + b2.title);
		System.out.println("b2.series : " + b2.series);
		System.out.println("b2.page : " + b2.page);
		
		Book b3 = new Book("신데렐라", 170); // ← 생성자 3
		System.out.println("b3.title : " + b3.title);
		System.out.println("b3.series : " + b3.series);
		System.out.println("b3.page : " + b3.page);
		
		Book b4 = new Book(5, "노인과 바다"); // ← 생성자 4
		System.out.println("b4.title : " + b4.title);
		System.out.println("b4.series : " + b4.series);
		System.out.println("b4.page : " + b4.page);
	}
}
```

```java
출력값
b1.title : 제목없음
b1.series: 1 
b1.page : 100

b2.title : 멘토시리즈 자바
b2.series: 1 
b2.page : 100

b3.title : 신데렐라 
b3.series: 1 
b3.page : 170

b4.title : 노인과 바다
b4.series: 5 
b4.page : 100
```

### **this와 this()**

- this는 인스턴스 자신을 가르키는 참조변수 , this()는 생성자를 뜻한다.

1. 객체 자신을 가리키는 참조변수 - 객체의 자원을 소비하기 위한 목적인 참조변수
- this 참조변수는 인스턴스가 바로 자기 자신을 참조하는데 사용하는 변수이다. this를 필드에 붙여서 사용하면, 중괄호 ‘ { }’ 안에서도 같은 이름의 매개변수와 필드를 구분해서 사용할 수 있다.

```java
class Student{
String name;
int age;
int studentID;

Student(String name, int age, int studentID) {
name = n;
age = a;
studentID = sid;

```

- 클래스로 선언된 name, age, studentID는 보다 직관적으로 명명되어 있는데, 생성자의 매개변수로 선언된 n, a, sid는 어떤 의미의 변수인지 작성자만 명확히 이해 할 수 있다. 그렇다고 필드와 같은 이름의 매개변수를 사용하면 지역변수가 클래스 필드보다 우선순위가 높아서, 대입연산자를 기준으로 왼쪽/오른쪽 변수 모두 매개변수를 뜻하게 된다. 즉 매개변수에 매개변수를 넣는 의미 없는 코드가 된다.
- 생성자의 매개변수로 인스턴스변수들의 초기값을 제공받는 경우가 많기 때문에 매개변수와 인스턴스변수의 이름이 일치하는 경우가 자주 있다. 이때 왼쪽코드와 같이 매개변수이름을 다르게 하는 것 보다 ‘this’를 사용해서 구별되도록 하는 것이 의미가 더 명확하고 이해하기 쉽다.
- 그래서 this 키워드를 사용한다.
- this의 사용 방법은 다음과 같다.

```java
this.필드 = 매개변수명;
```

```java
class Student{
String name;
int age;
int studentID;

Student(String name, int age, int studentID) {
this.name = name;
this.age = age;
this.studentID = studentID;
```

- this 키워드를 사용하면, Student 생성자를 다음과 같이 수정할 수 있다.
- ‘this’는 참조변수로 인스턴스 자신을 가리킨다.  참조변수를 통해 인스턴스의 멤버에 접근할 수 있는 것처럼, ‘this’로 인스턴스변수에 접근할 수 있다는것이다. 하지만  ‘this’를 사용할 수 있는 것은 인스턴스멤버뿐이다. static메서드(클래스 메서드)에서는 인스턴스 멤버들을 사용할 수 없는 것처럼 ‘this’ 역시 사용할 수 없다. 왜냐하면 static 메서드는 인스턴스를 생성하지 않고도 호출될 수 있으므로 staitic 메서드가 호출된 시점에 인스턴스가 존재하지 않을 수 있기 때문이다.

2.생성자에서 다른 생성자 호출하기 - this()

this()메서드는  같은 클래스 안에 있는 생성자 중 매개변수의 개수, 자료형, 순서에 맞는 다른 생성자를 호출하는 메서드로 생성자 내부에서만 사용할 수 있다.

<aside>
💡 생성자 오버로딩의 규칙이 있기 때문에, 별도로 명시하지 않아도 매개변수의 개수/자료형/순서를 가지고 원하는 생성자를 호출해 사용할 수 있다.

</aside>

```java
this(매개변수1, 매개변수2, ...) 
```

this()메서드를 사용하면 다음과 같이 사용할 수 있다.

```java
package section09;
 ...

	Phone(String brand, int series) {
		this.brand = brand;
		this.series = series;
		}

	Phone(String brand, int series, String color) {
		this(brand, series);
		this.color = color;
	}
}
```

- 매개변수를 2개 받는 생성자와 매개변수를 3개 받는 생성자는 사실 코드가 중복되고 있다. 중복되는 코드를 줄이기 위해 this()메서드를 활용할 수 있다.

```java
package section09;
 ...

	Phone(String brand, int series) {
		this.brand = brand;
		this.series = series;
		}

	Phone () {
	this( "아이폰", 13, "스페이스 그레이"); // 다른 생성자 호출
	}
```

<aside>
💡 this()메서드는 반드시 생성자의 첫줄에서만 사용할 수 있다.

</aside>

- 같은 클래스 내의 생성자들은 일반적으로 서로 관계가 깊은 경우가 많아서 이처럼 서로 호출하도록 하여 유기적으로 연결해주면 더 좋은 코드를 얻을 수 있다. 그리고 수정이 필요한 경우에 보다 적은 코드만을 변경하면 되므로 유지보수가 쉬워진다.
