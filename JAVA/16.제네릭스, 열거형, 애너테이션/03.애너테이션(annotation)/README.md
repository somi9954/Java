# 애너테이션(annotation)
- 프로그램의 소스코드 안에 다른 프로그램을 위한 정보를 미리 약속된 형식으로 포함시킨 것이 애너테이션이다.
- 애너테이션은 주석(comment)처럼 프로그래밍 언어에 영향을 미치지 않으면서도 다른 프로그램에게 유용한 정보를 제공할 수 있다는 장점이 있다.
- 애너테이션(annotation)의 뜻은 주석, 주해, 메모이다.

```java
@interface 애너테이션명{

}
```

```java
@Test   // 이 메서드가 테스트 대상임을 테스트 프로그램에게 알린다.
public void method() {
	....
}

'@Test'는 이 메서드를 테스트해야 한다는 것을 테스트 프로그램에게 알리는 역할을 하며, 
메서드가 포함된 프로그램 자체에는 아무런 영향을 미치지 않는다. 주석처럼 존재하지 않는 것이나 다름없다.
```

- 표준 에너테이션 : JDK에서 제공하며 주로 컴파일러를 위한 것으로 컴파일러에게 유용한 정보를 제공한다.
- 메타 에너테이션 : 새로운 애너테이션을 정의할 때 사용한다.

**에너테이션이란?**

- 자바에서 기본적으로 제공하는 표준 애너테이션(*가 붙은 것은 메타 애너테이션)
- 애너테이션설명 @Override 컴파일러에게 재정의 하는 메서드라는 것을 알린다.
- @Deprecated앞으로 사용되지 않을 것을 권장하는 대상에게 붙인다.
- @SuppressWarnings컴파일러의 특정 경고메세지가 나타나지 않게 해준다.
- @SafeVarargs지네릭스 타입의 가변인자에 사용한다.(JDK1.7)@FunctionalInterface함수형 인터페이스라는 것을 알린다.(JDK1.8)
- @Nativenative메서드에서 참조되는 상수 앞에 붙인다.(JDK1.8)@Target*애너테이션이 적용 가능한 대상을 지정하는데 사용한다.
- @Documented*애너테이션 정보가 @javadoc으로 작성된 문서에 포함되게 한다.
- @Inherited*애너테이션이 하위 클래스에 상속되도록 한다.
- @Retention*애너테이션이 유지되는 범위를 지정하는데 사용한다.
- @Repeatable*애너테이션을 반복해서 적용할 수 있게 한다.(JDK1.8)

**표준 애너테이션**
- 메서드 앞에만 붙일 수 있는 에너테이션
- 상위클래스의 메서드를 재정의 하는 것이라는 걸 컴파일러에게 알려주는 역할을 한다.
- 재정의할 떄 메서드 앞에 '@Override'라고 애너테이션을 붙이면, 컴파일러가 같은 이름의 메서드가 상위 클래스에 있는지 확인하고 없으면 에러메세지를 출력한다.
- 재정의할 때 메서드 앞에 '@Override'를 붙이는 것이 필수는 아니지만 알아내기 어려운 실수를 미연에 방지해 주므로 붙이는 것이 좋다.

- jdk에 정의되어 있는 기본 애너테이션

```java
@Override

@Deprecated

@SupreessWarning

@FunctionInterface

@Retention

@Target
```

**@Deprecated**
- '@Deprecated' 애너테이션이 붙은 대상은 다른 것으로 대체되었으니 더 이상 사용하지 않을 것을 권한다는 의미
- 예) java.util.Date 클래스의 대부분의 메서드에서는 '@Deprecated'가 붙어 있다.

```java
java.util.Date
	int getDate()
	Deprecated.
	As of JDK version 1.1, replaced by Calendar.get(Calendar.DAY_OF_MONTH).
	
	이 메서드 대신에 JDK1.1 부터 추가된 Calendar 클래스의  get()을 사용하라는 것
```

day16/AnnotationEx2.java

```java
package day16;

class NewClass {
	int newField;
	
	int getNewField() { return newField; }
	
	@Deprecated
	int oldField;
	
	@Deprecated
	int getOldField() { return oldField; }
}

public class AnnotationEx2 {
	public static void main(String[] args) {
		NewClass nc = new NewClass();
		
		nc.oldField = 10;  // @Deprecated가 붙은 대상을 사용 
		System.out.println(nc.getOldField()); // @Deprecated가 붙은 대상을 사용 
	} 
}

컴파일 결과 
D:\javaEx\lecture\src\day16>javac AnnotationEx2.java
Note: AnnotationEx2.java uses or overrides a deprecated API.
Note: Recompile with -Xlint:deprecation for details.
```

**@FunctionalInterface**
- '함수형 인터페이스(functional interface)'를 선언할 때, 이 애너테이션을 붙이면 컴파일러가 '함수형 인터페이스'를 올바르게 선언했는지 확인하고, 잘못된 경우 에러를 발생시킨다.
- 필수는 아니지만, 붙이면 실수를 방지할 수 있으므로 '함수형 인터페이스'를 선언할 때는 이 애너테이션을 붙이는 것이 좋다.
- 함수형 인터페이스는 추상 메서드가 하나뿐이어야 한다는 제약이 있다(18일차 - 람다식 참조)

```java
@FunctionalInterface
public interface Runnable {
	public abstract void run(); // 추상 메서드
}

```

**@SupressWarnings**
- 컴파일러가 보여주는 경고메시지가 나타나지 않게 억제해 준다.
- 주로 사용되는 것은 "deprecation", "unchecked", "rawtypes", "varargs" 정도 이다.
    - deprecation : "@Deprecated"가 붙은 대상을 사용해서 발생하는 경고를 억제
    - unchecked : 지네릭스로 타입을 지정하지 않았을 때 발생하는 경고를 억제
    - rawtypes : 지네릭스를 사용하지 않아서 발생하는 경고를 억제
    - varargs : 가변인자의 타입이 제네릭 타입일 때 발생하는 경고를 억제

```java
 @SupressWarnings("unchecked")  // 지네릭스와 관련된 경고를 억제 
 ArrayList list = new ArrayList(); // 지네릭 타입을 지정하지 않음 
 list.add(obj); // 경고 발생 
```

- 둘 이상의 경고를 동시에 억제하려면 배열에서처럼 중괄호{}를 추가로 사용해야 한다.

```java
@SuppressWarnings({"deprecation", "unchecked", "varargs"})
```

day16/AnnotationEx3.java
```java
package day16;

import java.util.ArrayList;

class NewClass2 {
	int newField;
	
	int getNewField() {
		return newField;
	}
	
	@Deprecated
	int oldField;
	
	@Deprecated
	int getOldField() {
		return oldField;
	}
}

public class AnnotationEx3 {
	@SuppressWarnings("deprecation") // deprecation관련 경고를 억제
	public static void main(String[] args) {
		NewClass2 nc = new NewClass2();
		
		nc.oldField = 10;
		System.out.println(nc.getOldField());
		
		@SuppressWarnings("unchecked") // 지네릭스 관련 경고를 억제
		ArrayList<NewClass2> list = new ArrayList(); // 타입을 지정하지 않음
		list.add(nc);
	}
}

```

**@SafeVarags**
- 메서드에 선언된 가변인자의 타입이 non-reifiable 타입일 경우, 해당 메서드를 선언하는 부분과 호출하는 부분에서 "unchecked"경고가 발생한다 해당 코드에 문제가 없다면 이 경고를 억제하기 위해 "@SafeVarargs"를 사용해야 한다.
 - 이 애너테이션은 static이나 final이 붙은 메서드에만 붙일 수 있다. 즉 오버라이드 될 수 있는 메서드에는 사용할 수 없다.
 - 지네릭스에서 살펴본 것과 같이 어떤 타입들은 컴파일 이후에 제거된다. 컴파일 후에도 제거되지 않는 타입을 reifiable타입이라 하고, 제거되는 타입을 non-reifiable타입이라고 한다.
 - 지네릭 타입들은 대부분 컴파일 시에 제거되므로 non-reifiable타입이다.
   
day16/AnnotationEx4.java
```java
package day16;

import java.util.Arrays;

class MyArrayList<T> {
	T[] arr;
	
	@SafeVarargs
	MyArrayList(T... arr) {
		this.arr = arr;
	}
	
	@SafeVarargs
	public static <T> MyArrayList<T> asList(T... a) {
		return new MyArrayList<>(a);
	}
	
	public String toString() {
		return Arrays.toString(arr);
	}
}

public class AnnotationEx4 {	
	public static void main(String[] args) {
		MyArrayList<String> list = MyArrayList.asList("1", "2", "3");
		
		System.out.println(list);
	}
}

```

**메타 애너테이션**
- 애너테이션을 위한 애너테이션
- 애너테이션을 붙이는 애너테이션으로 애너테이션을 정의할 때 애너테이션의 적용대상(target)이나 유지기간(retention)등을 지정하는데 사용된다.
- 메타 애너테이션은 "java.lang.annotation" 패키지에 포함되어 있다.

**@Target**
- 애너테이션이 적용 가능한 대상을 지정하는데 사용된다.
- **"@target"으로 지정할 수 있는 애너테이션 적용대상의 종류**대상 타입의미ANNOTION_TYPE애너테이션CONSTRUCTOR생성자FIELD필드(멤버변수, enum상수) - 기본자료형에 사용LOCAL_VARIABLE지역변수METHOD메서드PACKAGE패키지PARAMETER매개변수TYPE타입(클래스, 인터페이스, enum)TYPE_PARAMETER타입 매개변수TYPE_USE타입이 사용되는 모든 곳 - 참조자료형에 사용

```java
import static java.lang.annotation.ElementType.*;

@Target({FIELD, TYPE, TYPE_USE}) // 적용대상이 FIELD, TYPE, TYPE_USE
public @interface MyAnnotation { // MyAnnotation을 정의

}

@MyAnnotation  // 적용대상이 TYPE인 경우
class MyClass {
	@MyAnnotation  // 적용대상이 FIELD인 경우 
	int i; 
	
	@MyAnnotation // 적용대상이 TYPE_USE인 경우
	MyClass mc;
}

```

**@Retention**
- 애너테이션이 유지되는 기간을 지정하는데 사용된다.
- **애너테이션 유지정책(retention policy)의 종류**유지 정책의미 SOURCE소스 파일에만 존재, 클래스파일에는 존재하지 않음CLASS클래스 파일에 존재, 실행시에 사용불가, 기본값RUNTIME클래스 파일에 존재, 실행시에 사용가능
• SOURCE
         ◦ 자바코드에는 존재(Java) → 컴파일 이후에 제거 ⇒컴파일 시에 정보가 전달(컴파일러에게 전달)

    ◦ "@Override"나 "@SuppressWarnings"처럼 컴파일러가 사용하는 애너테이션은 유지 정책이 SOURCE이다. 컴파일러를 직접 작성할 것이 아니면 이 유지정책은 필요 없다.

```java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.SOURCE)
public @interface Override {}
```

- RUNTIME
  - 자바 코드에도 존재(Java) , 클래스 파일에서도 존재(Class) → 실행 중에 정보가 전달
  - 실행 시에 '리플렉션(reflection)'을 통해 클래스 파일에 저장된 애너테이션의 정보를 읽어서 처리할 수 있다.
  - "@FunctionalInterface"는 "@Override"처럼 컴파일러가 체크해주는 애너테이션이지만, 실행 시에도 사용되므로 유지 정책이 "RUNTIME"으로 되어 있다.

```java
 @Documented
 @Retention(RetentionPolicy.RUNTIME)
 @Target(ElementType.TYPE)
 public @interface FunctionalInterface {}
```

- CLASS
    - 자바 코드에도 존재(Java), 클래스 파일에도 존재(class) → 기본값, 정보 전달 X
    - 컴파일러가 애너테이션의 정보를 클래스 파일에 저장할 수 있게는 하지만, 클래스 파일이 JVM에 로딩될 때는 에너테이션의 정보가 무시되어 실행 시에 애너테이션의 정보를 얻을 수 없다.
    - CLASS가 기본값이지만 상기 사유로 잘 사용되지 않는다.
- 지역변수에 붙은 애너테이션은 컴파일러만 인식할 수 있으므로, 유지정책이 RUNTIME인 애너테이션을 지역변수에 붙여도 실행 시에는 인시되지 않는다. (지역변수는 함수가 호출될때 스택에 올라갈때 인식이 가능하므로)

**@Documented**
- 애너테이션에 대한 정보가 javadoc으로 작성한 문서에 포함되도록 한다.

```java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
public @interface FunctionalInterface {}
```

**@Inherited**
- 애너테이션을 하위 클래스에 상속되도록 한다,
- "@Inherited"가 붙은 애너테이션을 상위 클래스에 붙이면, 하위 클래스도 이 애너테이션이 붙은 것과 같이 인식된다.

```java

@Inherited // @SuperAnno가 하위클래스까지 영향 미치게
@interface SuperAnno {}

@SuperAnno
class Parent {}

class Child extends Parent {} // Child에 애너테이션이 붙은 것으로 인식

```

**@Repeatable**
- "@Repeatable"이 붙은 애너테이션은 여러 번 붙일 수 있다.

day16/AnnotationEx5.java
```java
package day16;

import java.lang.annotation.*;

@interface ToDos {
	ToDo[] value();
}

@Repeatable(ToDos.class)
 @interface ToDo {
	String value();
}

@ToDo("자바 공부")
@ToDo("자바스크립트 공부")
@ToDo("데이터베이스 공부")
public class AnnotationEx5 {
	
}

```

**@Native**
- 네이티브 메서드(native method)에 의해 참조되는 '상수 필드(constant field)'
- 네이티브 메서드는 JVM이 설치된 OS의 메서드를 말한다.
- 네이티브 메서드는 보통 C언어로 작성되어 있는데, 자바에서는 메서드의 선언부만 정의하고 구현은 하지 않는다.
- 그래서 추상 메서드 처럼 선언부만 있고 몸통이 없다.
- 네이티브 메서드는 자바로 정의되어 있기 대문에 호출하는 방법은 자바의 일반 메서드와 다르지 않지만 실제로 호출하는 것은 OS의 메서드이다.

```java
java.lang.Long 클래스에 정의된 상수 예

@Native public static final Long MIN_VALUE = .....

public class Object {
	private static native void registerNatives(); 
	
	static {
		registerNatives(); // 네이티브 메서드를 호출
	}
	
	protected native Object clone() throws CloneNotSupportedException;
	public final native Class<?> getClass();
	public final native void notify();
	public final native void notifyAll();
	public final native void wait(long timeout) throws InterruptedException;
	public native int hashCode();
	...
}
```

**애너테이션 타입 정의하기**
- "@"기호를 붙이는 것을 제외하면 인터페이스를 정의하는 것과 동일하다.
- 엄밀히 말하면 "@Override"는 애너테이션이고 'Override'는 '애너테이션'의 타입이다.

```java
@interface 애너테이션이름 {
	타입 요소이름(); // 애너테이션의 요소를 선언한다.
	...
}

```

**애너테이션의 요소**
- 애너테이션 내에 선언된 메서드를 '애너테이션의 요소(element)'라고 한다.
- 애너테이션에도 인터페이스처엄 상수를 정의할 수 있지만 디폴트 메서드는 정의할 수 없다.

```java
@interface TestInfo {
	int count();
	String testedBy();
	String[] testTools();
	TestType testType();  // enum TestType { FIRST, FINAL }
	DateTime testDate(); //  자신이 아닌 다른 애너테이션(@DateTime)을 포함할 수 있다.
}

@interface DateTime {
	String yymmdd();
	String hhmmss();
}

```

- 애너테이션의 요소는 반환값이 있고 매개변수는 없는 추상 메서드의 형태를 가지며, 상속을 통해 구현하지 않아도 된다.
- 애너테이션을 적용할 때 이 요소들의 값을 빠짐없이 지정해주어야 한다.
- 요소이름을 같이 적어서 적용하므로 순서는 상관 없다.

```java
@TestInfo(
	count = 3, testedBy="Kim",
	testTools={"JUnit", "AutoTester"},
	testType=TestType.FIRST,
	testDate=@DateTime(yymmdd="160101", hhmmss="235959")
)
public class NewClass {
	..
}
```

- 애너테이션의 각 요소는 기본값을 가질 수 있으며, 기본값이 있는 요소는 애너테이션을 적용할 때 값을 지정하지 않으면 기본값이 사용된다.

```java
@interface TestInfo {
	int count() default 1; // 기본값을 1로 지정
}

@TestInfo // @TestInfo(count=1)과 동일
public class NewClass { ... }
```

- 애너테이션 요소가 오직 하나뿐이고 이름이 value인 경우, 애너테이션을 적용할 때 요소의 이름을 생략하고 값만 적어도 된다.

```java

@interface TestInfo {
	String value();
}

@TestInfo("passed") // @TestInfo(value = "passed")와 동일
class NewClass { ... }
```

- 요소의 타입이 배열인 경우, 괄호{}를 사용해서 여러 개의 값을 지정할 수 있다.

```java
@interface TestInfo {
	String[] testTools();
}

@Test(testTools={"JUnit", "AutoTester"}) // 값이 여러 개인 경우
@Test(testTools="JUnit") // 값이 하나일 대는 괄호{} 생략가능
@Test(testTools={})  // 값이 없을 때는 괄호{}가 반드시 필요

```

- 기본값을 지정할 때도 마찬가지로 괄호{}를 사용할 수 있다.

```java

@interface TestInfo {
	String[] info() default {"aaa", "bbb"};  // 기본값이 여러 개인 경우, 괄호 {} 사용
	String[] info2() default "ccc";  // 기본값이 하나인 경우, 괄호 생략 가능
}

@TestInfo  // @TestInfo(info={"aaa", "bbb"}, info2="ccc")와 동일
@TestInfo(info2={}) // @TestInfo(info={"aaa", "bbb"}, info2={})와 동일
class NewClass { ... }

```

- 요소의 타입이 배열일 때에도 요소의 이름이 value이면, 요소의 이름을 생략할 수 있다.

```java
@interface SuppressWarnings {
	String[] value();
}

@SuppressWarnings(value={"deprecation", "unchecked"})
@SuppressWarnings({"deprecation", "unchecked"})
class NewClass { ... }
```

**java.lang.annotation.Annotation**
- 모든 애너테이션의 상위 클래스는 Annotation이다. 그러나 애너테이션은 상속이 허용되지 않으므로 명시적으로 Annotation을 상위 클래스로 지정할 수 없다.

```java

@interface TestInfo extends Annotation { // 에러. 허용되지 않는 표현
	int count();
	String testedBy();
	...
}

```

- Annotation은 애너테이션이 아니라 일반적인 인터페이스로 정의되어 있다.
- 모든 애너테이션의 상위 클래스인 Annotation인터페이스가 하기와 같이 정의되어 있으므로, 모든 애너테이션 객체에 대해 equals(), hashCode(), toString()과 같은 메서드를 호출할 수 있다.

```java
package java.lang.annotation;

public interface Annotation { // Annotation 자신은 인터페이스이다.
	boolean equals(Object obj);
	int hashCode();
	String toString();
	
	Class<? extends Annotation> annotationType(); // 애너테이션의 타입을 반환
}

```

**마커 애너테이션(Marker Annotation)**
- 값을 지정할 필요가 없는 경우, 애너테이션의 요소를 하나도 정의하지 않을 수 있다. Serializable이나 Cloneable인터페이스처럼, 요소가 하나도 정의되지 않은 애너테이션을 마커 애너테이션이라고 한다.

```java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.SOURCE)
public @interface Override {} // 마커 애너테이션. 정의된 요소가 하나도 없다.

@Target(ElementType.METHOD)
@Retention(RetentionPolicy.SOURCE)
public @interface Test {}  // 마커 에너테이션. 정의된 요소가 하나도 없다.

```

**애너테이션 요소의 규칙**
- 애너테이션 요소를 선언할때 반드시 지켜야 하는 규칙
  - 요소의 타입은 기본형, String, enum, 애너테이션, Class만 허용된다.
  - ()안에 매개변수를 선언할 수 없다.
  - 예외를 선언할 수 없다.
  - 요소를 타입 매개변수로 정의할 수 없다.

```java

@interface AnnoTest {
	int id = 100; // OK, 상수 선언, public static fiunal int id = 100;
	String major(int i, int j); // 에러, 매개변수를 선언할 수 없음
	String minor() throws Exception; // 에러, 예외를 선언할 수 없음
	ArrayList<T> list(); // 에러, 요소의 타입에 타입 매개변수 사용불가
}

```

day16/AnnotationEx6.java
```java
package day16;

import java.lang.annotation.*;

@Retention(RetentionPolicy.RUNTIME) // 실행시에사용가능하도록 지정
@interface TestInfo {
	int count() default 1;
	String testedBy();
	String[] testTools() default "JUnit";
	TestType testType() default TestType.FIRST;
	DateTime testDate();
}

@Retention(RetentionPolicy.RUNTIME) // 실행 시에 사용가능하도록 지정
@interface DateTime {
	String yymmdd();
	String hhmmss();
}

enum TestType { FIRST, FINAL }

@Deprecated
@TestInfo(testedBy="aaa", testDate=@DateTime(yymmdd="160101", hhmmss="235959"))
public class AnnotationEx6 {
	public static void main(String[] args) {
		// AnnotationEx6의 Class 객체를 얻는다.
		Class<AnnotationEx6> cls = AnnotationEx6.class;
		
		TestInfo anno = (TestInfo)cls.getAnnotation(TestInfo.class);
		System.out.println("anno.testedBy()=" + anno.testedBy());
		System.out.println("anno.testDate().yymmdd()" + anno.testDate().yymmdd());
		System.out.println("anno.testDate().hhmmss()=" + anno.testDate().hhmmss());
		
		for(String str : anno.testTools()) {
			System.out.println("testTools=" + str);
		}
		
		System.out.println();
		
		// AnnotationEx6에 적용된 모든 애너테이션을 가져온다.
		Annotation[] annoArr = cls.getAnnotations();
		
		for (Annotation a : annoArr) {
			System.out.println(a);
		}
	}
}

실행결과
anno.testedBy()=aaa
anno.testDate().yymmdd()160101
anno.testDate().hhmmss()=235959
testTools=JUnit

@java.lang.Deprecated(forRemoval=false, since="")
@day16.TestInfo(count=1, testType=FIRST, testTools={"JUnit"}, testedBy="aaa", testDate=@day16.DateTime(yymmdd="160101", hhmmss="235959"))
```
