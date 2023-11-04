# String 클래스

- 문자열을 처리하는 객체형 데이터 타입이다.
- String을 사용할 때 문자열을 생성자의 매개변수로 하여 생성하는 방식과 이미 생성된 문자열 상수를 가리키는 방식이 있다.

```java
String str1 = new String("abc"); // 생성자의 매개변수로 문자열 생성
String str2 = "test"; // 문자열 상수를 가리키는 방식

```

- 내부적으로 두 가지 방식은 큰 차이가 있습니다.
- new 예약어를 사용하여 객체를 생성하는 경우는 "abc" 문자열을 위한 메모리가 할당되고 새로운 객체가 생성됩니다.
- 하지만 str2 = "test"와 같이 생성자를 이용하지 않고 바로 문자열 상수를 가리키는 경우에는 str2가 기존에 만들어져 있던 "test"라는 문자열 상수의 메모리 주소를 가리키게 됩니다.
- 따라서 String str3 = "test" 코드를 작성하면 str2와 str3는 주소 값이 같게 됩니다.

![image](https://github.com/somi9954/Java/assets/137499604/20532526-23bd-4e64-b87d-d2c36f6bd6ad)


- test나 10, 20 등과 같이 프로그램에서 사용되는 상수값을 저장하는 공간을 **상수 풀(constant pool)** 이라고 합니다.

**String 클래스의 final char[]변수**

- 문자형 배열(char[])과 그에 관련된 메서드들이 정리되어 있다.

```java
public final class String implements java.io.Serializabel, Comparabel {
/** The value is used for character storage. */
private final char[] value;
...
```

- String 인스턴스가 갖고 있는 문자열은 읽어 올 수 만 있고 변경할 수는 없다.
- 이런 문자열의 특징을 **문자열은 불변(immutable)한다**라고 합니다.
- 프로그램에서 두 개의 문자열을 연결하면 둘 중에 하나의 문자열이 변경되는 것이 아니라 두 문자열이 연결된 새로운 문자열이 생성됩니다.

<aside>
💡Tip

jdk 8 까지는 String 객체의 값은 char[] 배열로 구성되어져 있지만, jdk 9부터 기존 char[]에서 byte[]을 사용하여 String Compacting을 통한 성능 및 heap 공간 효율(2byte -> 1byte)을 높이도록 수정되었다.

</aside>

```java
package day11.string;

public class StringTest2 {
	public static void main(String[] args) {

		String javaStr = new String("java");
		String androidStr = new String("android");
		System.out.println(javaStr);
		System.out.println("처음 문자열 주소 값: "+ System.identityHashCode(javaStr));

		javaStr = javaStr.concat(androidStr); //java 와 android 문자열의 연결

		System.out.println(javaStr);
		System.out.println("연결된 문자열 주소 값: " +System.identityHashCode(javaStr));
	}
}

실행결과

java
처음 문자열 주소 값: 1651191114
javaandroid
연결된 문자열 주소 값: 1586600255

```

- 두 개의 문자열 "java"와 "android"를 생성했습니다. 그리고 두 문자열을 연결하는 concat() 메서드를 호출했습니다.
- javaStr 변수 출력 결과를 보면 "javaandroid"로 연결되어 잘 출력되고 있습니다.
- 이 결과만 보면 "java" 문자열에 "android"문자열이 연결된 것 같지만, **문자열은 불편(immutable)하므로 javaStr 변수 값 자체가 변하는 것이 아니라 새로운 문자열이 생성**된 것입니다.

![image](https://github.com/somi9954/Java/assets/137499604/69087d9e-f7b5-4dd6-b999-f14220d2be9d)


**문자열 상수 풀(String Constant Pool)**

- Java는 문자열 상수 풀 또는 문자열 풀이라고 불리는 특수한 저장 공간을 가지고 있습니다. 문자열 상수 풀은 Java의 힙 영역에 존재하는 특수한 공간으로 문자열 리터럴을 저장하는 용도로 사용됩니다.
- 문자열 리터럴이 생성될 때마다 JVM은 해당 문자열이 문자열 상수 풀에 존재하는지 확인합니다. 문자열 상수 풀에 해당 문자열이 존재하지 않으면, 해당 문자열을 문자열 상수 풀에 저장하고 존재하면 저장하지 않습니다.

위 내용을 이해하기 쉽게 다음 소스 코드를 살펴봅시다.

```java
int num = 10;
boolean bool = false;
String str = "Hello";
```

- Java의 기본 타입(byte, char, short, int, boolean, long 등.. )은 스택(Stack)에 저장됩니다.
- 반면에, 참조 타입의 데이터는 힙(Heap)에 저장됩니다. 스택에 존재하는 변수는 힙에 존재하는 데이터를 참조합니다.

위 소스 코드를 그림으로 나타내면 다음과 같습니다.

![image](https://github.com/somi9954/Java/assets/137499604/0e94fb81-5e25-4433-844b-598084ff0848)


- 변수 num과 bool은 기본 타입이므로 데이터가 스택 영역에 존재합니다. 하지만, 변수 str의 타입은 String이므로 실제 데이터는 힙 영역에 존재하는 문자열 상수 풀에 존재합니다.

**문자 리터럴과 문자열(String) 리터럴**

- 빈문자열은 내용이 없는 문자열. 크기가 0인 char형 배열을 저장하는 문자열이다.
- 자바 소스파일에 포함된 모든 문자열 리터럴은 컴파일 시에 클래스 파일에 저장된다. 이때 같은 내용의 문자열  리터럴은 한번만 저장된다. 문자열 리터럴도 String인스턴스이고, 한번 생성하면 내용을 변경을 할 수 없다. 왜냐하면 하나의 인스턴스를 공유하면 되기 때문이다.

```java
문자 리터럴 : 작은따옴표로 문자 하나를 감싼 것. ex) 'A', 'B', 'C'
문자열 리터럴(String) : 큰따옴표로 두 문자 이상을 감싼 것. ex) "사랑", "믿음", "소망"

char ch = 'J';        // char ch = 'Java'; 이렇게 할 수 없음
String name = "Java"; // 변수 name에 문자열 리터럴 "Java"를 저장
```

- **문자열 리터럴**은 큰따옴표 안에 **아무런 문자도 넣지 않는 것을 허용**하며, 이를 **'빈 문자열(empty string)'**이라고 한다. 그러나 **문자 리터럴**은 작은따옴표 안에 **반드시 하나의 문자**가 있어야 한다.

```java
String str = " ";// 내용이 없는 빈 문자열char ch = '';// 에러. 작은따옴표 안에는 반드시 하나의 문자가 필요char ch = ' ';// 공백 문자(blank)로 변수 ch를 초기화
```

문자열 리터럴은 문자열을 생성할 수 있는 가장 기본적인 방법입니다.

```java
public static void main(String args[]) {
  String str1 = "Hello";
  String str2 = "World";
  String str3 = "Hello";
}
```

**[문자열 풀 동작 과정]**

**순서 1.** 프로그램이 실행되면, 문자열 상수 풀은 기본적으로 비어 있습니다. 따라서, 문자열 상수 풀에 문자열 "Hello"가 저장됩니다.

**순서 2.** JVM은 문자열 변수 str2에 문자열 "World"를 할당하기 전에 문자열 상수 풀에 문자열 "World"가 존재하는지 확인합니다. 문자열 상수 풀에 문자열 "World"가 존재하지 않으므로 문자열 "World"가 문자열 상수 풀에 저장되고 문자열 변수 str2는 참조 값을 가집니다.

**순서 3.** 첫 번째 순서에서 "Hello"라는 문자열이 문자열 상수 풀에 저장되었으므로 문자열 변수 str3는 동일한 참조 값을 가집니다.

위 소스 코드를 그림으로 나타내면 다음과 같습니다.

![image](https://github.com/somi9954/Java/assets/137499604/ad411818-d727-4185-96ca-3ce4ae3ccbab)


**[Java] 자바 문자열을 다루는 String 클래스 메소드 총정리**

String 클래스는 문자열의 추출, 비교, 찾기, 분리, 변환 등과 같은 다양한 메소드를 가지고 있습니다. 그중에서도 사용 빈도수가 높은 10가지 메소드를 소개합니다.

| 리턴 타입 | 메소드 이름(매개 변수) | 설명 |
| --- | --- | --- |
| char | charAt(int index) | 특정 위치의 문자를 리턴합니다. |
| boolean | equals(Object anObject) | 두 문자열을 비교합니다. |
| byte[] | getBytes() | byte[]로 리턴합니다. |
| byte[] | getBytes(Charset charset) | 주어진 문자셋으로 인코딩한 byte[]로 리턴합니다. |
| int | indexOf(String str) | 문자열 내에서 주어진 문자열의 위치를 리턴합니다. |
| int | length() | 총 문자의 수를 리턴합니다. |
| String | replace(CharSequence target, CharSequence replacement) | target 부분을 replacement로 대치한 새로운 문자열을 리턴합니다. |
| String | substring(int beginIndex) | beginIndex 위치에서 끝까지 잘라낸 새로운 문자열을 리턴합니다. |
| String | substring(int beginIndex, int endIndex) | beginIndex 위치에서 endIndex 전까지 잘라낸 새로운 문자열을 리턴합니다. |
| String | toLowerCase() | 알파벳 소문자로 변환한 새로운 문자열을 리턴합니다. |
| String | toUpperCase() | 알파벳 대문자로 변환한 새로운 문자열을 리턴합니다. |
| String | trim() | 앞뒤 공백을 제거한 새로운 문자열을 리턴합니다. |
| String | valueOf(int i)valueOf(double d) | 기본 타입 값을 문자열로 리턴합니다. |

### 문자 추출(charAt())

- 원하는 위치 문자를 문자열에서 추출할 수 있다.
- 인덱스란 0부터 ‘문자열 길이 -1’까지의 번호를 말한다.

```java
String subject = "자바 프로그래밍";
char charValue = subject.charAt(3);
```

“자바 프로그래밍” 문자열은 다음과 같이 인덱스를 매길 수 있습니다. **charAt(3)은 3번 인덱스 위치**에 있는 문자를 말합니다. 즉 **‘프’ 문자가 해당**됩니다.

| 자 | 바 |  | 프 | 로 | 그 | 래 | 밍 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |

```java
package section15;

public class EX15_08 {
	public static void main(String[] args) {
		
		String word = "1I2LOVE6YOU";
		
		// 문자열에서 숫자를 찾아 제거하고 문자만 출력
		String text = "";
		
		// length()는 해당 문자열의 길이를 반환해 주는 메서드
		for(int i = 0; i < word.length(); i++) {
			// charAt(index) 메서드는 문자열을 하나의 문자로 각각 반환
			char ch = word.charAt(i);
			int asciiNum = ch; // 문자를 아스키코드에 의한 10진수 값으로 변환
			
			// 소문자 a~z는 97~122, 대문자는 65~90 사이
			if((asciiNum >= 65 && asciiNum <= 90) || (asciiNum >= 97 && asciiNum <= 122)) {
				text += ch;
			} else {
				text += " ";
			}
		}
		
		System.out.println(text);
	}
}

출력값
I LOVE YOU
```

### 문자열 찾기(indexOf())

- 저장된 문자열 중에서 우리가  찾는 특정 단어 또는 문장의 시작 위치를 알려주는 메서드
- 찾는 단어가 없으면 -1을 반환한다.

```java
String subject = "자바 프로그래밍";
int index = subject.indexOf("프로그래밍");
```

index 변수에는 3이 저장되는데, “자바 프로그래밍”에서 “프로그래밍” 문자열의 인덱스 위치가 3이기 때문입니다.

| 자 | 바 |  | 프 | 로 | 그 | 래 | 밍 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |

indexOf( ) 메소드는 if문의 조건식에서 특정 문자열이 포함되어 있는지 여부에 따라 실행 코드를 달리할 때 자주 사용됩니다. -1 값을 리턴하면 특정 문자열이 포함되어 있지 않다는 뜻입니다.

```java
if( 문자열.indexOf("찾는문자열") != -1 ) {
    //포함되어 있는 경우
} else {
    //포함되어 있지 않은 경우
}
```

```java
package section15;

public class EX15_09 {
	public static void main(String[] args) {
		
		String str = "HelloWorld_MyWorld";
		// 처음 위치에서 검색
		System.out.println("World 단어 위치 : " + str.indexOf("World"));
		// 10번째 위치부터 시작하여 검색
		System.out.println("World 단어 위치 : " + str.indexOf("World", 10));
	}
}
출력값
World 단어 위치 : 5
World 단어 위치: 13
```

- 문자열에서 검색하는 단어의 마지막 위치를 찾고 싶을 때는 lastIndexOf()메서드를 사용한다. 해당 메서드는 뒤에서부터 검색하여 찾는 문자의 위치를 알려준다.

```java
lastIndexOf("apple");
System.out.println(str.lastIndexOf("apple"));
```

| a | p | p | l | e |   | m | a | n | g | o |  | a | p | p | l | e |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 |
- 위와 같이 글자가 위치할 경우 출력 결과는 마지막 단어의 시작점인 12번째가 출력된다.

### 문자열 잘라내기(substring())

- 원하는 위치에서 문자열을 잘라서 사용할 수 있는 메서드이다.
- 입력된 문자열 중에서 특정 위치의 문자를 추출할 수 있다.
- 매개 변수에 따라서 두가지 타입으로 존재한다.

```java
substring(int beginIndex)
substring(int beginIndex, int endIndex)
```

```java
String ssn = "880815-1234567";
String firstNum = ssn.substring(0, 6);
String secondNum = ssn.substring(7);
```

상기 코드에서 firstNum 변수값은 “880815”이고, secondNum 변수값은 “1234567”입니다. ssn.substring(0, 6)은 인덱스 0(포함)~6(제외) 사이의 문자열을 추출하는 것이고, substring(7)은 인덱스 7부터 끝까지 문자열을 추출합니다.

| 8 | 8 | 0 | 8 | 1 | 5 | – | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 |

```java
package section15;

public class EX15_11 {
	public static void main(String[] args) {
		//문자열 선언
		String str = "1234-5687";
		//4번째 위치부터 문장끝까지 가져온다.
		String subStr = str.substring(5);
		
		System.out.println("4번째 위치부터 추출 : " + subStr);
		
		//범위 내에서 문자를 추출한다
		String rangeStr = str.substring(0, 4);
		System.out.println("범위 내에서 추출 : " + rangeStr);
	}
}

출력값
4번 위치에서 추출 : 5687
범위 내에서 추출 : 1234
```

### 알파벳 소문자, 대문자 변경(toLowerCase(),toUpperCase())

- toLowerCase( ) 메소드는 문자열을 모두 소문자로 바꾼 새로운 문자열을 생성한 후 리턴합니다. 반대로 toUpperCase( ) 메소드는 문자열을 모두 대문자로 바꾼 새로운 문자열을 생성한 후 리턴합니다.

```java
String original = "Java Programming";
String lowerCase = original.toLowerCase();
String upperCase = original.toUpperCase();
```

- lowerCase 변수는 새로 생성된 “java programming” 문자열을 참조하고 upperCase 변수는 새로 생성된 “JAVA PROGRAMMING” 문자열을 참조합니다. 이때 원래 original 변수의 “Java Programming” 문자열이 변경된 것은 아닙니다.

![image](https://github.com/somi9954/Java/assets/137499604/4073df7e-80ac-42c3-a2ec-b39d5da14407)


- toLowerCase( )와 toUpperCase( ) 메소드는 영어로 된 두 문자열을 대소문자와 관계없이 비교할 때 주로 이용됩니다. 다음 예제에서는 두 문자열이 대소문자가 다를 경우 어떻게 비교하는지를 보여줍니다. equals( ) 메소드를 사용하려면 사전에 toLowerCase( )와 toUpperCase( )로 대소문자를 맞추어야 하지만, equalsIgnoreCase( ) 메소드를 사용하면 이 작업이 생략됩니다.

```java
public class String_toCaseTest {
 
    public static void main(String[] args) {
        // TODO Auto-generated method stub
        String str = "Banana Mango Apple";
        
        String substr1 = str.toLowerCase();
        String substr2 = str.toUpperCase();
        
        System.out.println(substr1);
        System.out.println(substr2);
    }
}
출력값
banana mango apple
BANANA MANGO APPLE
```

### 문자열 변환(replace()/replaceAll())

- 특정 문자 및 문자열을 원하는 단어로 변경해 주는 메서드이다.
- replace보다 기능상의 이점으로 replaceAll 을 주로 사용한다.

```java
//replace
String oldstr = "자바 프로그래밍";
String newstr = oldstr.replace("자바", "자바")
```

String 객체의 문자열은 변경이 불가능한 특성을 갖기 때문에 replace( ) 메소드가 리턴하는 문자열은 원래 문자열의 수정본이 아니라 완전히 새로운 문자열입니다. 따라서 newStr 변수는 다음 그림과 같이 새로 생성된 “JAVA 프로그래밍” 문자열을 참조합니다.

![image](https://github.com/somi9954/Java/assets/137499604/58ea6303-a18b-45d6-aff0-7d703ae14069)



```java
//replaceAll 
String replaceAllTest = "우리의 리플레이스의 리플레이스테스트";
        System.out.println( replaceAllTest.replaceAll("리플레이스","replaceAll") );
```

```java
package section15;

public class EX15_10 {
	public static void main(String[ ] args) {
		String str = "자바 프로그래밍은 어렵지만 자바를 배울수록 재미있습니다.";
		// 단어 ‘자바’를 ‘Java’로 변경
		String newStr = str.replaceAll("자바", "Java");
		
		System.out.println(str);
		System.out.println(newStr);
	}
}

출력값
자바 프로그래밍은 어렵지만 자바를 배울수록 재미있습니다.
자바 프로그래밍은 어렵지만 Java를 배울수록 재미있습니다.
```

### 문자열 앞뒤 공백 잘라내기(trim())

- trim( ) 메소드는 문자열의 앞뒤 공백을 제거한 새로운 문자열을 생성하고 리턴합니다. 다음 코드를 보면 newStr 변수는 앞뒤 공백이 제거된 새로 생성된 “자바 프로그래밍” 문자열을 참조합니다. trim( ) 메소드는 앞뒤의 공백만 제거할 뿐 중간의 공백은 제거하지 않습니다.

```java
String oldStr = " 자바 프로그래밍 ";
String newStr = oldStr.trim();
```

- trim( ) 메소드를 사용한다고 해서 원래 문자열의 공백이 제거되는 것은 아닙니다. 다음 그림에서 oldStr.trim( )은 oldStr의 공백을 제거하는 것이 아닙니다.

![image](https://github.com/somi9954/Java/assets/137499604/7d102f83-0058-4554-84cf-cc0a3c0c4f85)


```java
String str = " 문자열에 공백이 있습니다. ";		
System.out.println(str);

str = str.trim();
System.out.println(str);

출력값
 문자열에 공백이 있습니다.
문자열에 공백이 있습니다.
```

### 문자열 변환(valueOf())

- valueOf( ) 메소드는 기본 타입의 값을 문자열로 변환하는 기능을 가지고 있습니다. String 클래스에는 매개 변수의 타입별로 valueOf( ) 메소드가 다음과 같이 오버로딩되어 있습니다.

```java
static String valueOf(boolean b)
static String valueOf(char c)
static String valueOf(int i)
static String valueOf(long l)
static String valueOf(double d)
static String valueOf(float f)
```

```java
package 기본기03;

 

public class T17 {

 

        public static void main(String[] args) {

 

               String a = "1234";

               String b = String.valueOf(10);

               String c = String.valueOf(a);

               String d = String.valueOf(true);

               String e = String.valueOf(false);

               //String.valueOf는 int형이든 double형이든 boolean형이든 String객체로 만든다.

              

               System.out.println(a);

               System.out.println(b);

               System.out.println(c);

               System.out.println(d);

               System.out.println(e);

 

              

               System.out.println(a + b);

               System.out.println(a + b + c);

               System.out.println(c + d);

               System.out.println(c + d + e);

               //a,b,c,d,e 모두 String 객체이므로 +연산자로 합치면 글자를 합친 결과와 같다.

        }
}
출력값
1234
10
1234
true
false
123410
1234101234
1234true
1234truefalse

```

### 문자열 길이(length())

length( ) 메소드는 문자열의 길이(문자의 수)를 리턴합니다.

```java
String subject = "자바 프로그래밍";
int length = subject.length();
```

length 변수에는 8이 저장됩니다. subject 객체의 **문자열 길이는 공백을 포함해서 8개**이기 때문입니다.

| 자 | 바 |  | 프 | 로 | 그 | 래 | 밍 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |

### 문자열 비교(equlas())

- 기본 타입(byte, char, short, int, long, float, double, boolean) 변수의 값을 비교할 때에는 == 연산자를 사용합니다. 그러나 문자열을 비교할 때에는 == 연산자를 사용하면 원하지 않는 결과가 나올 수 있습니다.

```java
String strVar1 = new String(“신민철”);
String strVar2 = “신민철”;
String strVar3 = “신민철”;
```

- 자바는 문자열 리터럴이 동일하다면 동일한 String 객체를 참조하도록 되어 있습니다. 그래서 strVar2와 strVar3은 동일한 String 객체를 참조합니다. 그러나 strVar1은 new 연산자로 생성된 다른 String 객체를 참조합니다.

![image](https://github.com/somi9954/Java/assets/137499604/ee886e4b-57c8-4053-999b-d9fd6edf0044)


이 경우 변수 strVar1과 strVar2의 == 연산은 false를 산출하고 strVar2와 strVar3의 == 연산은 true를 산출합니다. == 연산자는 각 변수에 저장된 번지를 비교하기 때문에 이러한 결과가 나옵니다.

```java
strVar1 == strVar2 //false
strVar2 == strVar3 //true
```

만약 두 String 객체의 문자열만을 비교하고 싶다면 == 연산자 대신에 equals( ) 메소드를 사용해야 합니다. 원래 equals( )는 Object 클래스의 번지 비교 메소드이지만, String 클래스가 재정의해서 문자열을 비교하도록 변경했습니다.

```java
strVar1.equals(strVar2) //true
strVar2.equals(strVar3) //true
```

```java
//문자열 비교 == 연산자
public class compare {
    public static void main(String[] args) {
        String s1 = "abcd";
        String s2 = new String("abcd");
		
        if(s1 == s2) {
            System.out.println("두개의 값이 같습니다.");
        }else {
            System.out.println("두개의 값이 같지 않습니다.");
        }
    }
}
출력값
두 값이 같지 않습니다.
```

```java
//문자열 비교 equals
public class compare {
    public static void main(String[] args) {
        String s1 = "abcd";
        String s2 = new String("abcd");
		
        if(s1.equals(s2)) {
            System.out.println("두개의 값이 같습니다.");
        }else {
            System.out.println("두개의 값이 같지 않습니다.");
        }
    }

출력값
두개의 값이 같습니다.
```

**join() 과 Stringjoiner**

- join은 여러 문자열 사이에 구분자를 넣어서 결합한다. 구분자로 문자열을 자르는 split()와는 반대이다.

```java
 String.join( "단어 사이에 넣고자 하는 텍스트 또는 기호", 변수명)
```

```java
public static void main(String[] args) {

    String A [] = {"Tiger", "Bear", "Lion"};
    
    String B = String.join("&", A));  // 배열의 단어 사이에 "&"을 넣고 결합
    
    System.out.println(B);
   
    // 배열의 단어를 합쳐서 문자열로 돌려줌	
}
출력값
Tiger&Bear&Lion
```

- 하나의 문장을 가지고 split( ) 메서드로 분리했다가 join( ) 메서드로 다시 합치는 것도 가능하다.

```java
public static void main(String[] args) {

    String A = "Tiger,Bear,Lion"; // 변수 A에 한 개의 문자열 저장
    
    String B [] = A.split(",");  // 배열 B에 split()으로 나눈 결과를 A에 저장
    
    String C = String.join("-", B);
    // "-"를 기준으로 배열의 단어를 병합할 수 있도록 join() 메서드 이용
    
    System.out.println(C); // 
}
출력값
Tiger-Bear-Lion
```

- StringJoiner는 java.util.StringJoiner클래스를 사용하여 문자열을 결합할 수 있다.
- StringJoiner의 객체를 생성하고 생성시 파라미터로 구분자를 넣어주고 add( ) 메서드로 내용만 추가하면 끝이다
- StringJoiner의 참조변수를 인쇄하면 add로 추가한 내용을 구분자를 기준으로 하나의 문자열로 합친 값을 얻는다.

```java
public static void main(String[] args) {
		
	StringJoiner test = new StringJoiner("-");
        // StringJoiner의 객체 생성. 이때 매개변수로 구분자를 넣어 줌.
    
	String A [] = {"Bear", "Tiger", "Lion"};  // A의 배열 선언 및 값 저장
		
	test.add(A[0]);// add 메서드로 StringJoiner의 인스턴스에 A배열의 단어 차례대로 저장
	test.add(A[1]);
	test.add(A[2]);
		
	System.out.println(test);
}
출력값
 Bear-Tiger-Lion //구분자를 넣어서 배열을 하나의 문자열로 통합해 반환
```

- 이것만 보면 Join ( )과 다를 바 없어보인다.  하지만 StringJoiner는 파라미터값을 더 전달해주면 문자열의 접두 부분과 접이 부분에 내용을 추가해줄 수 있다.
- StringJoiner의 객체를 생성할 때 아래와 같이 파라미터 값을 주면 된다.
- **new StringJoiner("구분자", "접두부분", "접미부분");** 과 같이 주면 문자열에 해당 내용이 반영된다.

```java
public static void main(String[] args) {
		
	StringJoiner test = new StringJoiner("-", "[", "]");
        // StringJoiner의 객체 생성. 
        // 이때 매개변수로 구분자와 문자열의 접두, 접미에 들어갈 텍스트 또는 기호를 준다.
    
	String A [] = {"Bear", "Tiger", "Lion"};  // A의 배열 선언 및 값 저장
		
	test.add(A[0]);// add 메서드로 StringJoiner의 인스턴스에 A배열의 단어 차례대로 저장
	test.add(A[1]);
	test.add(A[2]);
		
	System.out.println(test);
}
출력값
[Bear-Tiger-Lion] // StringJoiner의 객체 생성 때 파라미터로 넣었던 구분자, 접두, 접미 부분의 기호가 하나의 문자열로 통합되어서 출력
	
```
