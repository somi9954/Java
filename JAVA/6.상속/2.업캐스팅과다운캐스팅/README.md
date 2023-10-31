## 자바의 참조형 캐스팅

하나의 데이터 타입을 다른 타입으로 바꾸는 것을 타입 변환 또는 **형변환(캐스팅)** 이라고 한다.

자바의 데이터형은 두가지로 나눠진다

- 기본형(primitive type) - Boolean Type(boolean) = Numeric Type(short, int, long,  float, double,char)

- 참조형(reference type) - Class Type  - interface Type - Array Type - Enum Type - 그 외 다른 것…

**기본형이든 참조형이든 하나의 타입이다. 즉 서로 타입간의 형변환이 가능하다.**

기본적으로 자바에선 대입 연산자 ‘=’에서 변수와 값 서로 양쪽의 타입이 일치하지 않으면 할당이 불가능하다. 프로그램에서 값의 대입이나 연산을 수행할 때는 같은 타입끼리만 가능하기 때문이다.

기본형의 캐스팅은 보통  “**데이터 손실**”을 막기 위해 동작한다.

```java
1) long a = 10.233; //컴파일 에러
2) long a = (long)10.233; //캐스팅
```

1)과 같이 컴파일 에러가 나는 이유는 int형 데이터를 담는 a 라는 그릇에 소수점이 포함된 10.233이라는 수를 넣으려고 할때 소수점 아래 0.233라는 데이터가 손실이 되기 때문이다. 이러한 코드는 실제로 동작할 때 개발자가 의도하는 대로 동작될 가능성이 없어지고 직관성을 깨뜨린다. 하지만 개발자가 이 형태에 대해 이해하고 있으며 데이터 손실이 일어나도 상관 없다면 2)와 같이 캐스팅이 가능하다.

클래스는 reference 타입으로 분류되 참조형 캐스팅(업캐스팅 / 다운캐스팅) 이라고 불리운다.

![image](https://github.com/somi9954/Java/assets/137499604/62042e93-cc01-4d04-af18-21d197dabe35)


출처 :https://natejin.tistory.com/34

부모클래스의 객체는 자식 클래스의 멤버를 모두 가지고 있지 않다. 즉 참조변수의 형변환은 사용할 수 있는 멤버의 갯수를 조절하는것이다. 예를 들어 기본형 타입의 형변환 (실수 → 정수)는 값 (8.5 → 8)으로 바뀌게 된다. 그렇지만 객체 형변환의 멤버 갯수만  달라지게 된다. 참조 캐스팅은 이러한 클래스의 멤버 구성 관점에서 판별하면 쉬울것이다.

### 참조형의 업캐스팅& 다운캐스팅

```java
class pizza {
    
    public void pizza1() {
        System.out.println("피자!");
    }
    
}
 
// pizza 클래스를 상속받는 potato 클래스
class potato extends pizza {
    
    public void potato1() {
        System.out.println("포테이토피자!");
    }
    
}
```

- **참조형의 업캐스팅**

```java
public static void main(String[] args) {
        
       < 업 캐스팅 >
 
        // 서브클래스potato 인스턴스 생성
        potato p = new potato();
        p.pizza1();  // 슈퍼클래스로부터 상속받은 메서드
        p.potato1();  // 서브클래스 메서드
        
        
        pizza z; // 슈퍼클래스 타입 레퍼런스 변수 선언
        z = p; // 서브클래스 인스턴스를 슈퍼클래스 타입 레퍼런스 변수에 저장
               // 서브-> 슈퍼 이므로 자동형변환이 일어난다.(업캐스팅)
             
        z.pizza1(); // 슈퍼클래스 메서드 
//        z.potato1(); // 서브클래스 메서드 => 에러 발생!
                       // potato 인스턴스에는 pizza1() , potato1() 메서드가 존재하지만
                       // pizza(슈퍼클래스) 타입으로 참조할 경우에는 pizza 클래스에 정의된 멤버만 접근 가능하다
```

- **참조형의 다운캐스팅**

```java
< 다운 캐스팅 >
 
        // 슈퍼클래스 pizza 인스턴스 생성
        pizza z2 = new pizza();
        z2.pizza1();
        
        potato p2; // 서브클래스 타입 레퍼런스 변수 선언
        
//        p2 = z2; // 슈퍼클래스 인스턴스를 서브클래스 타입 레퍼런스 변수에 저장 => 컴파일 에러 발생!
                 // => 형변환 연산자를 사용하여 강제 형변환이 필요하다!
        
        p2 = (potato)z2; // 형변환 연산자를 사용하여 서브클래스 타입으로 강제 형변환 => 실행 시 오류 발생
        
        p2.pizza1(); // 슈퍼클래스 인스턴스에 실제 존재하는 메서드
//        p2.potato1(); // 서브클래스 내에 potato1() 메서드가 정의되어 알고있지만, 
                        // 슈퍼클래스에는 없는 메서드이다.
                        // p2 에 슈퍼클래스 인스턴스를 저장했으므로! 오류발생 !
        
        System.out.println("-----------------------------------------------------------");
        
        < 업 캐스팅 후 다운 캐스팅 > 
 
        pizza p3 = new potato(); // 업캐스팅(자동형변환)
        p3.pizza1(); // 업캐스팅 시 상속된 메서드는 호출 가능하지만
//        p3.potato1(); // 서브클래스에서 정의한 메서드는 호출 불가
        
//        potato z3 = p3; // 다운캐스팅
        potato z3 = (potato)p3; // 형변환 연산자 사용 필수!
        z3.pizza1(); //  상속받은 메서드, 서브클래스 메서드 모두 호출 가능
        z3.potato1(); //  참조영역이 늘어난다.
```

### 업캐스팅(Upcasting)

- **캐스팅**이란 **타입을 변환하는 것**을 말하며 형변환이라고도 한다. 자바의 상속 관계에 잇는 부모와 자식 클래스 간에는 서로 간에 형변환이 가능하다.
- 업캐스팅이란 자식 클래스의 객체가 **부모 클래스의 타입으로 형변환 되는 것**을 말한다.
- 업캐스팅은 항상 가능하다. 생략시에 컴파일러에 의해 자동 캐스팅이 된다.
- 하나의 인스턴스(=부모클래스)로 서브 클래스들을 전부 관리 할 수 있어서 업캐스팅을  사용한다. 즉 부모 클래스로 관리하면 자바의 다형성(메서드를 각각  다른 형태로 사용)을 이용해 부모 클래스를 여러가지 클래스로 만들 수 있다.
- 부모 클래스로 캐스팅 된다는 것은 멤버의 갯수 감소를 의미한다. 즉 자식 클래스에서만 있는 속성과 메서드는 실행하지 못한다.  업캐스팅을 하고 메소드를 실행할때 만일 자식 클래스에서 오버라이딩 한 메서드가 있을 경우, 부모 클래스의 메서드가 아닌 오버라이딩 된 메서드가 실행되게 된다.

```java
public class Person {
	String name;
	int id;
	public Person(){
		name="홍길동";
	}
}
public class Student extends Person {
	String grade;
	String major;
	public Student(){
		grade="4학년";
		major="computer";
	}
}
```

```java
public static void main(String[] args) {
      Person person2 = new Student();
        // person의 참조변수 name, id만 확인 할 수있음.
        Student student = new Student();
				Person person = student;
        System.out.println(person.id);
      //  System.out.println(person.major);  //컴파일 오류
    }
```

```java
//출력값
홍길동

```

<aside>
💡 Person person = (Person)student 를 통해 업 캐스팅 되었다.
Person타입이므로 자신의 클래스에 속한 멤버와 메서드만 접근할 수 있다. 
업 캐스팅을 하였더니 객체내의(Student 객체)모든 멤버와 메서드에 접근할 수 없다. 
(int id ; 오류발생) 업 캐스팅은 명시적 타입 캐스팅을 하지 않아도 객체 앞에 묵시적 형변환을 수행할 수 있다.

</aside>

### 다운캐스팅(Downcasting)

- 다운 캐스팅의 목적은 업캐스팅한 객체를 되돌리는데 있다. 다음과 같이 업캐스팅이 되지 않는
  부모 객체 person일 경우, 그대로 (student)person 다운 캐스팅하면 (java.lang.ClassCastException)
   가 발생하게 된다.
- 다운캐스팅은 거꾸로 부모 클래스가 자식 클래스 타입으로 캐스팅 되는것이다.
- 다운캐스팅은 캐스팅 연산자 괄호를 생략할 수 없다.

```java
public class Person {
	String name;
	String id;
	public Person(){
		name="홍길동";
	}
}
public class Student extends Person {
	String grade;
	String major;
	public Student(){
		grade="4학년";
		major="computer";
	}
}
```

```java
/** public static void main(String[] args) {
        Person person = new Person();
        Student student2 = (Student)person;
        System.out.println(student2.name);
        System.out.println(student2.id);
   */    
public static void main(String[] args) {
        Person person = new Student(); //업캐스팅 선행
        Student student2 = (Student)person ; //다운캐스팅
        student2.name = "김이름";
        student2.id = "1234567";
        System.out.println(person.name);
        System.out.println(person.id); //다운캐스팅 후에는 id 까지 접근이 가능하다.

    }

```

```java
//출력값
김이름
1234567
```

### instanceof 연산자

어느 객체의 변수가 어느 클래스의 타입인지 판별해 true, false  를 반환해준다. 주의할 점은 instanceof 연산자는 객체에 대한 클래스(참조형)타입에서만 사용할 수 있다.(int, double 같은 primitive 타입에서 사용불가능)

instanceof 연산자는 다음과 같이 작성한다.

```java
if(A instanceof B) { // A 는 참조변수(객체), B 는 클래스명(타입)
// 형변환이 가능한 관계이므로 변환 수행
} else {
// 절대로 형변환이 불가능한 관계이므로 변환 수행 X
}
```

```java
class HandPhone {
	String modelName;
	String phoneNumber;
	
	public HandPhone(String modelName, String phoneNumber) {
		super();
		this.modelName = modelName;
		this.phoneNumber = phoneNumber;
	}
	
	public void call() {
		System.out.println("전화 기능!");
	}
	
	public void sms() {
		System.out.println("문자 기능!");
	}
		
}

class SmartPhone extends HandPhone {
	String osName;

	// 모델명, 전화번호, 운영체제명을 전달받아 초기화하는 생성자 정의
	// => 모델명과 전화번호는 슈퍼클래스의 생성자를 통해 대신 초기화 수행
	public SmartPhone(String modelName, String phoneNumber, String osName) {
		super(modelName, phoneNumber);
		this.osName = osName;
	}
	
	public void kakaoTalk() {
		System.out.println("카톡 기능!");
	}
}
```

```java
public class Ex2 {

	public static void main(String[] args) {
	
		SmartPhone sp = new SmartPhone("갤럭스s23", "010-1234-5678", "안드로이드");
		
		// 호출 가능한 메서드 : 3개
		sp.call();
		sp.sms();
		sp.kakaoTalk();
		
		// sp 는 SmartPhone 입니까? YES
		// => sp is a SmartPhone? = sp instanceof SmartPHone
		if(sp instanceof SmartPhone) {
			System.out.println("sp 는 SmartPhone 이다!");
			// sp 를 SmartPhone 타입 변수에 저장이 가능하다!
			SmartPhone phone = sp;
		}
		
		System.out.println("------------------------------");
		
		// 업캐스팅 가능 대상 확인
		// sp 는 HandPhone 입니까? YES
		if(sp instanceof HandPhone) {
			System.out.println("sp 는 HandPhone 이다!");
			System.out.println("그러므로 sp 를 HandPhone 으로 형변환 가능하다!");
			
			// sp -> HandPhone 타입(hp)으로 변환
			HandPhone hp = sp; // 업캐스팅 = 묵시적(자동) 형변환
			System.out.println("sp는 HandPhone 이 가진 모든 기능을 포함한다!");
			System.out.println("따라서, 업캐스팅 후에도 HandPhone의 기능 사용 가능");
			
			hp.call(); // HandPhone 의 기능인 전화기능과 
			hp.sms();  // 문자 기능을 사용할 수 있으나
//			hp.kakaoTalk(); // SmartPhone 의 기능은 사용을 포기해야 한다!
		} else {
			System.out.println("sp 는 HandPhone 이 아니다!");
		}
		
		System.out.println("------------------------------------------");
		
		// 다운캐스팅 가능 대상 확인
		// 슈퍼클래스 타입 인스턴스 생성
		HandPhone hp = new HandPhone("애니콜", "011-222-2222");
		
		// hp 는 SmartPhone 입니까? NO!
		if(hp instanceof SmartPhone) {
			System.out.println("hp는 SmartPhone 이다!");
		} else {
			System.out.println("hp는 SmartPhone 이 아니다!");
			System.out.println("그러므로 SmartPhone 으로 변환 불가능!");
			System.out.println("hp는 SmartPhone 이 가진 기능을 모두 포함하지 못함!");
		}
		
		System.out.println("----------------------------------");
		
		// 다운캐스팅 가능 대상 확인(가능한 경우)
		// SmartPhone -> HandPhone 타입(hp2)으로 업캐스팅
		HandPhone hp2 = new SmartPhone("갤럭스s23", "010-1234-5678", "안드로이드");
		
		// 업캐스팅 후에는 참조 영역 축소로 접근 범위가 줄어들게 됨
		hp2.call();
		hp2.sms();
//		hp2.kakaoTalk(); // 접근 불가!
		
		// hp2는 SmartPhone 입니까? YES
		if(hp2 instanceof SmartPhone) {
			System.out.println("hp2는 SmartPhone 이다!");
			System.out.println("그러므로 hp2는 SmartPhone 으로 형변환 가능!");
			
//			SmartPhone sp2 = hp2; // 자동 형변환 불가능
			SmartPhone sp2 = (SmartPhone)hp2; // 강제 형변환 필요
			
			System.out.println("hp2는 SmartPhone 이 가진 모든 기능을 포함한다!");
			
			sp2.call(); // HandPhone 의 기능인 전화 가능과
			sp2.sms(); // 문자 기능을 사용할 수 있으며
			sp2.kakaoTalk(); // SmartPhone 의 기능도 다시 사용이 가능해진다!
		} else {
			System.out.println("hp2는 SmartPhone 이 아니다!");
		}
	
```
