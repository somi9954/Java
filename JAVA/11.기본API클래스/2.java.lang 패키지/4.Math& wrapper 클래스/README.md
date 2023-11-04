# Math 클래스

- 기본적인 수학계산에 유용한 메서드로 구성되어 있다.
- Math클래스의 생성자는 접근 제어자가 private 이기 때문에 다른 클래스에서 Math인스턴스를 생성할 수 없도록 되어 있다 왜냐하면 클래스 내에서 인스턴스변수가 하나도 없어서 인스턴스를 생성할 필요가 없기 때문이다.
- 객체를 선언하지 않고 바로 사용할 수 있도록 해당 클래스가 제공하는 모든 메서드는 모두 정적 메서드(static)로 이루어져있다.
- 2개의 상수만 정의해 놓았다.

```java
public static final double E = 2.7182818284590452354;  //자연로그의 밑
public static final double PI = 3.14159265358979353846; //원주율 
```

**Math 클래스의 메소드는 다음과 같다.**

<table>
  <tr>
    <th>메서드</th>
    <th>설명</th>
  </tr>
  <tr>
    <td>static double random()</td>
    <td>0.0 이상 1.0 미만의 범위에서 임의의 double형 값을 하나 생성하여 반환함.</td>
  </tr>
  <tr>
    <td>
      static double abs(double a)<br>
      static double abs(float a)<br>
      static double abs(int a)<br>
      static double abs(long a)<br>
    </td>
    <td>전달된 값이 음수이면 그 값의 절댓값을 반환하며, 전달된 값이 양수이면 인수를 그대로 반환함.</td>
  </tr>
  <tr>
    <td>static double ceil(double a)</td>
    <td>전달된 double형 값의 소수 부분이 존재하면 소수 부분을 무조건 올리고 반환함.</td>
  </tr>
  <tr>
    <td>
     static double floor(double a)
    </td>
    <td>전달된 double형 값의 소수 부분이 존재하면 소수 부분을 무조건 버리고 반환함.</td>
  </tr>
  <tr>
    <td>
    static long round(double a)<br>
    static int round(float a)  <br>
    </td>
    <td>전달된 값을 소수점 첫째 자리에서 반올림한 정수를 반환함.</td>
  </tr>
    <tr>
    <td>static double rint(double a)</td>
    <td>전달된 double형 값과 가장 가까운 정수값을 double형으로 반환함.</td>
  </tr>
     <tr>
    <td>
      static double max(double a, double b) <br>
      static float max(float a, float b) <br>
      static long max(long a, long b)  <br>
      static int max(int a, int b) <br>
    </td>
    <td>전달된 두 값을 비교하여 큰 값을 반환함.</td>
  </tr>
    <tr>
    <td>
      static double min(double a, double b)
      static float min(float a, float b)
      static long min(long a, long b)
      static int min(int a, int b)
    </td>
    <td>전달된 두 값을 비교하여 작은 값을 반환함.</td>
  </tr>
    <tr>
    <td>static double pow(double a, double b)</td>
    <td>전달된 두 개의 double형 값을 가지고 제곱 연산을 수행하여, ab을 반환함.</td>
  </tr>
  <tr>
    <td>
     static double sqrt(double a)</td>
    <td>전달된 double형 값의 제곱근 값을 반환함.</td>
  </tr>
    <tr>
    <td>
      static double sin(double a)
      static double cos(double a)
      static double tan(double a)
    </td>
    <td>전달된 double형 값에 해당하는 각각의 삼각 함숫값을 반환함.</td>
  </tr>
    <tr>
    <td>static double toDegrees(double angrad)</td>
    <td>호도법의 라디안 값을 대략적인 육십분법의 각도 값으로 변환함.</td>
  </tr>
    <tr>
    <td>static double toRaidans(double angdeg)</td>
    <td>육십분법의 각도 값을 대략적인 호도법의 라디안 값으로 변환함.</td>
  </tr>
    <tr>
    <td>static int subtractExact(int a, int b)	</td>
    <td>전달 된 인수값의 차이를 반환. b-a</td>
  </tr>
    <tr>
    <td>static long subtractExact(long a, long b)</td>
    <td>전달 된 인수값의 차이를 반환. b-a</td>
  </tr>
</table>

### **1. abs() 메소드**

Math 클래스의 abs() 메소드는 인자로 넘긴 데이터의 절댓값을 반환해줍니다. 전달된 값이 양수이면 전달된 값 그대로 반환합니다.

```java
import java.lang.Math;
 
public class Sample
{
    public static void main(String[] args)
    {
        System.out.println(Math.abs(-10));   // 출력값 : 10
        System.out.println(Math.abs(0));     // 출력값 : 0
        System.out.println(Math.abs(10));    // 출력값 : 10
    }
}
```

### **2. random() 메소드**

random() 메소드는 0.0~1.0 사이의 임의의 double형 데이터를 생성하여 반환합니다. 해당 메소드를 사용하여 특정 범위의 난수를 발생시킬 수 있습니다.

```java
import java.lang.Math;
 
public class Sample
{
    public static void main(String[] args)
    {
        System.out.println((int)(Math.random() * 10));     // 0~9 사이 난수 발생
        System.out.println((int)(Math.random() * 100));  // 0~99 사이 난수 발생   
        System.out.println((int)(Math.random() * 1000)); // 0~999 사이 난수 발생    
    }
}
```

random()메서드를 사용하여 그냥 값을 받아 보면 출력 데이터의 범위는 다음과 같다.

```java
0 <= x < 1
```

이대로는 의미 있는 값으로 사용하기 힘들기 때문에 다음과 같은 작업을 해야한다.

1) 랜덤값에 곱셈을  하여 정수화를 한다.

```java
int randValue = (int)(Math.random()* 30)
```

2)값의 범위를 1부터 하기 위해서 곱셈 결과에 1을 더한다.

```java
int ranValue= (int)(Math.random()*30 )+ 1
```

최종범위는 1 ≤ x < 30으로 반환하는 수식이 된다.

### **3. max(), min() 메소드**

전달된 데이터 중 더 큰 수와 더 작은 수를 반환해주는 메소드입니다.

```java
import java.lang.Math;
 
public class Sample
{
    public static void main(String[] args)
    {
        System.out.println(Math.max(10,100)); // 100
        System.out.println(Math.min(10,100)); // 10
    }
}
```

### 4.****floor() 메소드, rint()메소드, ceil() 메소드와 round() 메소드****

자바 내림, 올림, 반올림이 가능한 메소드이다.

rint() 메소드는 가장 가까운 값을 반환한다.

```java
System.out.println(Math.ceil(10.0)); // 10.0 
System.out.println(Math.ceil(10.1)); // 11.0
System.out.println(Math.ceil(10.000001)); // 11.0 
System.out.println(Math.floor(10.0)); // 10.0
System.out.println(Math.floor(10.9)); // 10.0 
System.out.println(Math.round(10.0)); // 10 
System.out.println(Math.round(10.4)); // 10 
System.out.println(Math.round(10.5)); // 11
System.out.println(Math.rint(10.8)); // 11.0 반올림된다.
System.out.println(Math.rint(12.1)); // 12.0 내림
System.out.println(Math.rint(15.5)); // 16.0 .5의 경우 가장 가까운 짝수 값으로 반올림하기 때문에 16.0으로 반올림된다.
```

### **5. pow() 메소드와 sqrt() 메소드**

pow()는 제곱, sqrt()는 제곱근 반환할 수 있게 도와주는 메소드이다.

```java
System.out.println((int)Math.pow(5, 2));// 25
System.out.println((int)Math.sqrt(25));// 5
```

### **5. pow() 메소드와 sqrt() 메소드**

수치의 부호를 받아오는 메소드이다.

인수가 0이면 0, 인수가 0보다 크면 1.0 인수가 0보다 작으면 -1.0으로 반환한다.

```java
package com.devkuma.basic.math;

public class MathSignum {
    public static void main(String[] args) {
        double plus = Math.signum(100); // 1.0
        double zero = Math.signum(0); // 0.0
        double minus = Math.signum(-100); // -1.0

        System.out.println(plus);
        System.out.println(zero);
        System.out.println(minus);
    }
}
실행 결과:
1.0
0.0
-1.0
```

| 입력값 | signum() 반환값 |
| --- | --- |
| 100(양수) | 1 |
| 0(영) | 0 |
| -100(음수) | -1 |

# wrapper클래스

- 매개 변수가 객체거나 반환값이 객체인 경우

```java
public void setValue(Integer i) { ... } // 객체를 매개변수로 받는 경우
public Integer returnValue() { ... } // 반환 값이 객체인 경우
```

- 기본 자료형을 객체로 다루기 위한 클래스를 wrapper클래스라고 한다.

자바의 기본 자료형에 대응하여 제공되는 wrapper클래스의 종류는 다음과 같다.

| 기본형 | Wrapper 클래스 |
| --- | --- |
| boolean | Boolean |
| byte | Byte |
| char | Character |
| short | Short |
| int | Integer |
| long | Long |
| float | Float |
| double | Double |
- 생성자의 매개변수로 문자열을 제공할 때, 각 자료형에 알맞은 문자열을 사용해야 한다. 예를 들어 ‘new Interger(”1.0”); ‘ 과 같이 하면 NumberFormatException이 발생한다.

### Integer 클래스 사용하기

- int 자료형을 감싼 클래스
- Integer 클래스의 생성자는 다름과 같이 특정 정수를 매개변수로 받는 경우와 문자열을 받는 경우 두 가지가 있습니다.

```java

class Integer {
.... 변수, 메서드..
Integer(int value) { ... } // 특정 정수를 매개변수로 받는 경우
Integer(String s) { ... } // 특정 문자열을 매개변수로 받는 경우
... 변수, 메서드
}
```

- Integer 클래스는 int 자료형과 특성이 그대로 구현되어 있습니다. 사용 가능한 최대값과 최솟값이 static 변수로 정의되어 있습니다.
- 대부분의 Wrapper 클래스가 위 Integer 클래스의 정의와 크게 다르지 않습니다.
- Integer 클래스는 멤버 변수로 기본 자료형 int를 가지고 있고, int 값을 객체로 활용할 수 있는 여러 메서드를 제공합니다.
- int value는 final 변수 이며, 한번 생성되면 변경할 수 없습니다.

### Integer 클래스의 메서드

- intValue() : Integer 클래스 내부의 int 자료형 값을 가져오기 위해 사용

```java
Integer iValue = new Integer(100);
int myValue = iValue.intValue(); // int값 가져오기 myValue 값을 출력하면 100이 출력됨

```

- valueOf() 정적 메서드 : 정수나 문자열을 바로 Integer 클래스로 반환받을 수 있습니다.

```java
Integer number1 = Integer.valueOf("100");
Integer number2 = Integer.valueOf(100);

```

- parseInt() : 문자열이 어떤 숫자를 나타낼 때, 문자열에서 int 값을 바로 가져와서 반환할 수 있습니다.

```java
int num = Integer.parseInt("100");

```

- PARSEINT(STRING S) : **String to int.** 문자열을 int형으로 변환한다. 어쩌면 Integer에서 가장 많이 쓰이는 메소드

```java
String str = "123";
int num = Integer.parseInt(str);
```

- TOSTRING(INT I):int to String. 반대로 int를 String으로 변환한다.

```java
int num1 = 123;
String str1 = Integer.toString(num1);
```

- TOBINARAYSTRING(INT I):10진수를 2진수로 변환해 String으로 리턴한다.

int를 String으로 변환해 **toCharArray()**나 **charAt()**으로 찢고, 하나씩 빼는 방법도 있지만,그런 과정을 생략할 수 있어 편리하다.

다만 음수는 제대로 작동하지 않는 것 같아 보인다.

```java
String str2 = Integer.toBinaryString(num);
System.out.println("2진수: "+str2);
```

>> 2진수: 1111011

- TOOCTALSTRING(INT I):10진수->8진수로 바꿔 반환한다.

```java
String str3 = Integer.toOctalString(num);
System.out.println("8진수: "+str3);
```

>> 8진수: 173

- TOHEXSTRING(INT I) :10진수->16진수로 바꿔서 반환한다.

```java
String str4 = Integer.toHexString(num);System.out.println("16진수: "+str4);
```

>> 16진수: 7b

- PARSEINT(STRING S, INT RADIX) : **parseInt()**를 이용하여, 2진수를 10진수로 변환할수도 있다.

```java
int temp = Integer.parseInt(str2, 2);System.out.println("2진수->10진수: "+temp);
```

>> 2진수->10진수: 123

같은 방법으로 8진수->10진수 또한 가능하다.

```java
System.out.println("8진수->10진수: "+Integer.parseInt(str3, 8));
```

>> 8진수->10진수: 123

- MAX(INT A, INT B) : 둘 중 큰 수를 반환한다. 인자를 받아 큰 수와 작은 수를 구별해 처리해야 할 때 유용하다.

**min(int a, int b)**도 가능하다.

```java
System.out.println("더 큰 수 : "+ Integer.max(3, 5));
```

>> 더 큰 수 : 5

- BITCOUNT(INT I) :해당 숫자(i)를 2진수로 변환한 후, 1의 개수를 알아서 구해준다.

예를 들어 123 을 2진수로 변환하면 1111011인데 그럼 6개가 나오게 된다.

```java
System.out.println("2진수의 1 개수 : "+ Integer.bitCount(num1));
```

>> 2진수의 1 개수 : 6

```java
package section15;

public class EX15_14 {
	public static void main(String[] args) {
		// 정수형 타입 선언
		// 생성자를 통한 선언은 JDK 1.9부터 사용하지 않는 것을 권장
		Integer num01 = new Integer(10);
		Integer num02 = Integer.valueOf(10); // nem01 대신 num2 방법으로 사용
		
		// 실수형 타입 선언
		Double doubleNum01 = Double.valueOf(30.11);
		
		// 문자형 타입 선언
		Character ch = Character.valueOf('A');
		
		System.out.println("정수형1 : " + num01);
		System.out.println("정수형2 : " + num02);
		System.out.println("실수형 : " + doubleNum01);
		System.out.println("문자형 : " + ch);
	}
}
실행결과
정수형1 : 10
정수형2 : 10
실수형 : 30.11
문자형 : A
```

- 다른 Wrapper 클래스의 사용방법도 비슷합니다.

### 오토박싱(AutoBoxing)과 오토언박싱(AutoUnBoxing)

- 클래스를 사용할 때 객체를 선언한 후에 사용해야 한다. Wrapper 클래스도 데이터 타입이지만 기본적으로 클래스이기 때문에 객체를 선언해서 사용해야 한다.
- 기본 타입의 데이터를 Wrapper 클래스의 인스턴스로 변환하는 과정을 박싱(boxing)이라고 한다.
- 반대로 Wrapper 클래스의 인스턴스에 저장된 값을 기본 타입의 데이터로 꺼내는 과정을 언박싱(unboxing)이라고한다.

![image](https://github.com/somi9954/Java/assets/137499604/3f8428e6-b4c6-4925-8aab-14aefccdc8d3)

- JDK 1.5 부터는 박싱과 언박싱이 필요한 상황에 자바 컴파일러가 자동으로 처리해 주는데 이를 **오토박싱**과 **오토언박싱**이라고 한다.
- 문자 타입의 데이터를 숫자 타입의 데이터로 변경할 수 있는 기능이 있다.
- Wrapper 클래스의 ‘타입.parse(타입)(String s)’ 형식의 메서드와 ‘타입.valueOf()’메서드를 사용한다. 전자는 반환값이 기본형이고 후자는 반환값이 래퍼 클래스 타입이라는 차이가 있다.

![image](https://github.com/somi9954/Java/assets/137499604/0516bd78-f0ae-4359-a23b-500bcd3bfb7d)


```java
package exam01;

public class autoboxing_autounboxing {
    public static void main(String[] args) {

    // int형 숫자를 래퍼클래스 Integer 객체로 전환하는 것 : 박싱
    Integer num = new Integer(17);

    // 래퍼클래스 Integer 객체를 int형 숫자로 되돌리는 것 : 언박싱
    int n = num.intValue();

    // 오토박싱, char형 문자를 래퍼클래스에 할당하면 자동으로 래퍼클래스 Character 객체로 변환됨
    Character ch = 'X'; // Character ch = new Character('X'); 자동으로 이뤄짐

    // 오토언박싱, 래퍼클래스 Character 객체를 char형 변수에 할당하면 자동으로 char형 문자로 변환됨
    char c = ch;        // char c = ch.charValue(); 자동으로 이뤄짐

    /*<추가예시>*/
    //기본자료형 중 int형 값을 래퍼클래스를 이용해 래퍼객체로 만드는 박싱
    Integer it1 = new Integer(11);
    Integer it2 = new Integer(22);
    System.out.println(it1 + it2);  // 래퍼객체지만 덧셈이 정상적으로 수행됨
    System.out.println();

    //컴파일 중 자동으로 오토박싱이 일어나는 코드
    Integer it3 = 11;  	  	// Integer it3 = new Integer(11) 자동으로 일어남
    Integer it4 = 22;    	// Integer it4 = new Integer(22) 자동으로 일어남
    System.out.println(it3 + it4); // 래퍼객체지만 덧셈이 정상적으로 수행됨
    System.out.println();

    //컴파일 중 자동으로 오토언박싱이 일어나는 코드, 래퍼객체를 기본자료형 변수에 할당 할 때
    int it5 = new Integer(11) ; // new Integer(11) -> 11
    double d = new Double(1.1); // new Double(1.1) -> 1.1

    // int형 값 - Integer 래퍼객체 간의 연산 혹은 교차 할당이 아주 정상적으로 작동하는 예시
    Integer a1 = new Integer(11);
    int b1 = 22;
    System.out.println(a1 + b1);
    System.out.println();

    Integer a2 = 11;
    int b2 = new Integer(22);
    System.out.println(a2 + b2);
    System.out.println();
    }
}
```

```java
package exam01;

public class exam {
        public static void main(String[] args) {

            //언제 레퍼클래스를 사용하는가?
            int t = 100;
            String s = String.valueOf(t);// 정수를 문자열로 변환
            System.out.println(s);
						System.out.println();
            //100+"" -> 이것도 결과는 문자열임

            int x = Integer.parseInt("100"); // 문자를 정수로 변환해주는 역할을 하는데 기본형 int 로 반환함
            int y = Integer.parseInt("200");
            System.out.println(x+y);		// 300
            System.out.println();

            double z = Double.parseDouble("1.1");
            System.out.println(z); 			// 1.1
            System.out.println();

            //문자를 정수형으로 변환할 수 있는 메소드를 제공하는 래퍼클래스
            Integer t2 = Integer.valueOf("100");
            Integer u = Integer.valueOf("200");
            System.out.println(t+u);		// 300
            System.out.println();

            // 문자열 숫자 정수형으로 변환하여 총합구하기
            String[] arr2 = {"10","20","30","40","50"};
            int sum = 0;
            for(String s2 : arr2){
                sum += Integer.parseInt(s2);
            }
            System.out.println("총합:"+sum);
            System.out.println();

            // 문자열을 숫자만 분리해서 총합구하기
            String[] arr3 = {"슬기:80", "크리스탈:90", "아이유:40"};
            sum = 0;
            for(int i = 0; i< arr3.length; i++) {
                int index = arr3[i].indexOf(":");
                String s3 = arr3[i].substring(index+1);
                sum += Integer.parseInt(s3);
            }
            System.out.println("총합:"+sum);
        }
    }
```

![image](https://github.com/somi9954/Java/assets/137499604/d6d17125-13bb-4892-a6a3-cd0aecb8a3ee)
