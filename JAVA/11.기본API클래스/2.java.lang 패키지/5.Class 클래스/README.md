# class 클래스

- 클래스의 정보가 담겨 있는 객체
- 자바의 모든 클래스와 인터페이스는 컴파일되고 나면 class 파일로 생성됩니다.
- 예를 들어 a.java 파일이 컴파일되면 a.class 파일이 생성되고, 이 class 파일에는 클래스나 인터페이스에 대한 변수, 메서드, 생성자 등의 정보가 들어 있습니다.
- Class 클래스는 컴파일된 class파일에 저장된 클래스나 인터페이스 정보를 가져오는 데 사용합니다.

**class 클래스의 메소드**

forName() : 파라미터로 넘어온 클래스명의 객체를 찾아 Class 클래스를 반환한다.

getName() : 객체의 클래스명을 반환한다.

newInstance() : 객체의 클래스 인스턴스를 생성하여 반환한다.

getSuperclass() : 슈퍼(부모)클래스명을 반환한다.

getFields() : 클래스내에 변수(필드)들을 필드 리스트로 반환한다.

### Class 클래스란?

모르는 클래스의 정보를 사용할 경우 우리가 클래스의 정보를 직접 찾아야 합니다. 이때 Class 클래스를 활용합니다.

### Class 클래스를 선언하고 클래스 정보를 가져오는 방법

1. Object 클래스의 getClass() 메서드 사용하기

```java
String s = new String();
Class c = s.getClass(); // getClass() 메서드 반환형은 Class

```

1. 클래스 파일 이름을 Class 변수에 직접 대입하기

```java
Class c = String.class;

```

1. Class.forName("클래스 이름") 메서드 사용하기

```java
Class c = Class.forName("java.lang.String");

```

- 1번의 경우 Object에 선언한 getClass() 메서드는 모든 클래스가 사용할 수 있는 메서드입니다. 이 메서드를 사용하려면 이미 생성된 인스턴스가 있어야 합니다.
- 2,3번의 경우에는 컴파일된 클래스 파일이 있다면 클래스 이름만으로 Class 클래스를 반환받습니다.

```java
package day11.classex;

public class Person {
	private String name;
	private int age;

	public Person(){}

	public Person(String name){
		this.name = name;
	}

	public Person(String name, int age){
		this.name = name;
		this.age = age;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}
}

```

```java
package day11.classex;

public class ClassTest {
	public static void main(String[] args) throws ClassNotFoundException {

		Person person = new Person();
		Class pClass1 = person.getClass();  //Object 의 getClass() 메소드 사용
		System.out.println(pClass1.getName());

		Class pClass2 = Person.class;    // 직접 class 파일 대입
		System.out.println(pClass2.getName());

		Class pClass3 = Class.forName("day11.classex.Person"); // 클래스 이름으로 가져오기
		System.out.println(pClass3.getName());           //이름과 일치하는 클래스가 없는경우 ClassNotFoundException 발생함
	}
}

실행결과

day11.classex.Person
day11.classex.Person
day11.classex.Person

```

- Class 클래스를 통하여 클래스 정보를 알 수 있습니다.

### Class 클래스를 활용해 클래스 정보 알아보기

```java
package day11.classex;

import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.Method;

public class StringClassTest {
	public static void main(String[] args) throws ClassNotFoundException {

		Class strClass = Class.forName("java.lang.String");

		Constructor[] cons = strClass.getConstructors();
		for(Constructor c : cons){
			System.out.println(c);
		}
		System.out.println();
		Field[] fields = strClass.getFields();
		for(Field f : fields){
			System.out.println(f);
		}
		System.out.println();
		Method[] methods = strClass.getMethods();
		for(Method m : methods){
			System.out.println(m);
		}
	}
}

실행결과

public java.lang.String(java.lang.StringBuffer)
public java.lang.String(java.lang.StringBuilder)
public java.lang.String(byte[],int,int,java.nio.charset.Charset)
public java.lang.String(byte[],java.lang.String) throws java.io.UnsupportedEncodingException
public java.lang.String(byte[],java.nio.charset.Charset)
public java.lang.String(byte[],int,int)
public java.lang.String(byte[])
public java.lang.String(char[],int,int)
public java.lang.String(char[])
public java.lang.String(java.lang.String)
public java.lang.String()
public java.lang.String(byte[],int,int,java.lang.String) throws java.io.UnsupportedEncodingException
public java.lang.String(byte[],int)
public java.lang.String(byte[],int,int,int)
public java.lang.String(int[],int,int)

...

```

- Class 클래스와 java.lang.reflect 패키지에 있는 클래스를 활용하면 클래스 이름만 알아도 클래스의 생성자, 메서드 등의 정보를 알 수 있습니다.

### Class.forName()을 사용해 동적 로딩 하기

- 대부분의 클래스 정보는 프로그램이 로딩될 떄 이미 메모리에 있습니다.
- 예를들면 어떤 회사에서 개발한 시스템이 있는데, 그 시스템은 여러 종류의 데이터베이스를 지원합니다. 오라클, MySQL, MS-SQL 등등 여러 데이터베이스를 연동할 수 있습니다. 그렇다고 이 시스템을 구동할 떄 어떤 데이터 베이스와 연결할지만 결정되면 해당 드라이버만 로딩하면 됩니다. 회사에서 사용하는 데이터베이스 정보는 환경파일에서 읽어올 수 있고 다른 변수 값으로 받을 수도 있습니다.
- 즉, 프로그램 실행 이후 클래스의 로딩이 필요한 경우 **동적 로딩(dynamic loading)** 방식을 사용합니다.
- 자바는 Class.forName() 메서드를 동적 로딩으로 제공합니다.

```java
Class pClass = Class.forName("classex.Person");
                             (패키지명을 포함한 클래스명)

return ->class
```

- forName() 메서드를 살펴보면 매개변수로 문자열을 입력받습니다. 이때 입력받는 문자열을 변수로 선언하여 변수 값만 바꾸면 다른 클래스를 로딩할 수 있습니다.
- 앞에서 설명했듯이 여러 데이터베이스 드라이버 중 필요한 드라이버의 값을 설정 파일에서 읽어 문자열 변수로 저장한다면, 설정 파일을 변경함으로써 필요한 드라이버를 간단하게 로딩합니다.

```java
String className = "classex.Person";
Class pClass = Class.forName(className);

```

- 위와 같이 작성하고 className 변수에 다른 문자열을 대입하면 필요에 따라 로딩되는 클래스를 동적으로 변경할 수 있습니다.

### forName() 메서드를 사용할 때 유의할 점

- forName("클래스 이름")의 클래스 이름이 문자열 값이므로 **문자열에 오류가 있어도(Person의 P가 소문자라든가) 컴파일할 때는 그 오류를 알 수 없습니다.** 결국 프로그램이 실행되고 메서드가 호출될 떄 클래스 이름에 해당하는 클래스가 없다면 ClassNotFoundException이 발생합니다. 따라서 **동적 로딩 방식은 컴파일 할 때 오류를 알 수 없습니다.**
