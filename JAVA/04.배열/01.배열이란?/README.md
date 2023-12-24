# 배열(Array)

: 동일한 자료형을 저장할 저장 공간이 필요한 경우 일일이 변수를 선언하면 적지 않은 품이 든다. 이를 해결 하기 위해 ‘배열’을 사용한다.

- 동일한 자료형 + 물리적 나열 구조(순차자료구조)
- 각 요소의 순서를 쉽게 예측 → [ ] 인덱스 연산자

## 배열 선언, 배열 생성, 초기화

### 배열 선언 : 여러 변수를 한꺼번에 선언

   [ ] : 인덱스 연산자를 사용

   인덱스 : 배열의 위치를 가리키는 숫자

   배열의 순서는 0부터 시작하는 순서 번호 배열의 마지막 항목의 인덱스는 배열 크기 -1

자바에서 배열을 선언하는 방법은 다음과 같습니다.

```java
자료형[] 배열변수명;
자료형 배열변수명[];
```

예를 들어 배열은 다음과 같이 선언합니다.

```java
int intArray[];
char charArray[];
String name[];
```

또는  다음과 같이 선언합니다.

```java
int[] intArray;
char[] charArray;
String[] name;
```

### 배열 생성

 배열의 객체를 생성하려면 목록의 값을 이용하거나 New 연산자를 사용한다.

```java
자료형[] 배열변수명 = new 자료형[공간의 갯수];
자료형 배열변수명[] = new 자료형[공간의 갯수];
```

자바에서 배열을 생성하는 방법은 다음과 같습니다.

```java
int Array[] = new int[10];
int numbers[] = new int[5];
int score[] = new int[3];
char charArray[] = new char[20];
```

     또는 다음과 같이 생성합니다.

```java
int[] Array = new int[10];
int[] numbers = new int[5];
int[] score = new int[3];
char[] charArray = new char[20];
```

     int numbers[] =new int[5];

- 연산자 new에 의해서 메모리의 빈 공간에 5개의 int형 데이터를 저장할 수 있는 공간이 할당된다
- 할당된 공간은 자동적으로 int의 기본값인 0으로 초기화 된다.
- 대입연산자 ‘=’에 의해 배열의 주소가 int형 배열 참조변수 numbers에 저장된다.

![image](https://github.com/somi9954/Java/assets/137499604/a16726b2-144b-4573-ae41-7dc8baabad14)


### 배열 초기화

자바에서 초기화 방법은 다음과 같습니다.

```java
자료형[] 배열명 = new 자료형[] { 값1, 값2, 값3 ... };
		
자료형[] 배열명 = { 값1, 값2, 값3, 값4 ... };
	
자료형[] 배열명;
배열명 = new 자료형[] { 값1, 값2, 값3 ... }; ( O ) 
	
배열명 = {값1, 값2, 값3 ... } (X)
```

예를 들어 배열의 초기화 다음과 같이 선언합니다.

```java
int[] score = new int[5]; // int 타입의 값 5개가 저장될 빈 공간 생성
        score[0] = 10; // 각 빈공간에 값을 초기화
        score[1] = 20;
        score[2] = 30;
        score[3] = 40;
        score[4] = 50;
  for(int i = 0 ; i < score.length ; i++){
            score[i] = i * 10 + 50;
							}
    // for문으로 배열을 순차적으로 순회에 값을 넣어주는 방법도 있다.
  int[] score = new int[5];
        for(int i = 0 ; i < score.length ; i++){
            score[i] = i * 10 + 50;
							}
        
     
```

<aside>
💡 .length 속성
인덱스의 범위를 넘어가는 값을 인덱스로 주는 경우 ArrayIndexOutOfBoundsException이 발생한다.
자바에서는 JVM이 모든 배열의 길이를 별도로 관리하며 '.length'를 사용하여 배열의 길이에 대한 정보를 얻을 수 있다.

</aside>

**타입별 배열의 초기값**

![image](https://github.com/somi9954/Java/assets/137499604/b2a32f08-a5c3-4897-953e-09176d4fb28d)


```java
public class Ex05 {
    public static void main(String[] args) {
        int[] nums1 = new int[4];
        System.out.println(Arrays.toString(nums1));

        double[] nums2 = new double[4];
        System.out.println(Arrays.toString(nums2));

        boolean[] bools = new boolean[4];
        System.out.println(Arrays.toString(bools));

				String[]  strs = new String[4];
        System.out.println(Arrays.toString(strs));

    }
}
출력값
[0, 0, 0, 0]
[0.0, 0.0, 0.0, 0.0]
[false, false, false, false]
[null, null, null, null]
```

### 배열의 생성 및 초기화 출력

배열의 생성 및 초기화는 다음과 같습니다.

```java
import java.util.Arrays;

int[] score = new int[]{10, 20, 30, 40, 50}; 
int[] score = {10, 20, 30, 40, 50}; // new int[] 생략가능

        for(int i = 0 ; i < score.length ; i++){
            score[i] = i * 10 + 50;
					}
				 System.out.println(score);
         System.out.println(Arrays.toString(score)); 

//출력값
[I@723279cf
[50, 60, 70, 80, 90]
```

<aside>
💡 score 출력시 메모리에 있는 배열의 16진수 주소값  (타입@주소)으로 출력이 된다. 따라서 for 문을 이용해서 배열 각 원소들을 순회하여 출력하도록 하드코딩 해주거나, 아니면 자바에서 제공해주는 Arrays.toString(); 메서드를 이용해서 배열을 문자열 형식으로 만들어 출력할 수도 있다.

</aside>
<br>
<aside>
💡 Arrays 클래스는  프로그램을 개발하는 데 사용할 수 있는 유용한 유틸리티 클래스가 다수 포함되어 있는 java.util 패키지에 속해 있으며, 배열을 다루기 위한 다양한 메소드가 포함되어 있다. Arrays 클래스의 모든 메소드는 static 메소드이므로 따로 객체를 생성하지 않고도 바로 사용할 수 있는 특징이 있다. 다만 Arrays 클래스의 메소드를 사용하고 싶다면 상단에 반드시 import 문으로 java.util 패키지를 불러와야 한다.

</aside>

## 레퍼런스 변수와 배열

**레퍼런스 변수 ? 배열의 주소, 배열에 대한 주소값을 가지는 변수**

1. 배열에 대한 레퍼런스 변수 intArray 선언

```java
int intArray []
// 배열 타입, 배열에 대한 레퍼런스 변수, 배열선언
```

<aside>
💡 배열 선언시 [ ]안에 크기를 지정하면 안된다.

</aside>

- 주소값이 주어지기는 했지만 아직 생성되지 않은 상태
- NULL값을 갖는다고 생각
- 공간이 할당 되지 않음

2. 배열 생성

```java
intArray = new int [5]
// 배열에 대한 레퍼런스 변수, 배열 생성, 타입, 원소의 개수
```

- 이 배열에 대한 레퍼런스 값(주소값)을  intArray에 저장 방식이다.

1. 배열 초기화

```java
intArray = {10, 20, 30, 40, 50}; //배열에 10,20,30,40,50를 원소로 넣었음 정수이므로 타입 int사용
double doubleArray[] = {0.01, 0.02}//실수형이므로 타입 double 사용

```

1. 배열 인덱스와 배열 원소 접근

```java
int intArray[] = new int [5];// 원소가 5개인 배열 생성. 인덱스는 0~4
intArray[0] = 5; //원소 0에 5저장. 
intArray[3] = 1; //원소 3에 1저장. 
int n = intArray[3]; //원소 3의 값을 읽어서 n에 저장. n은 1이 됨.(세번째줄에서 1넣었음) 
```

1. 래퍼런스 치환과 배열 공유

```java
int intArray[] = new int[5];
int myArray[] = intArray; // 래퍼런스치환. myArray는 intArray와 동일한 배열 참
```

레퍼런스 즉 배열에 대한 주소만 복사된다. 그 결과 myArray는 intArray와 동일한 레퍼런스 값을 가지게 되어 inArray의 배열을 공유하게 된다. myArray는 intArray의 배열 원소를 마음대로 접근할 수 있다.

## 문자 저장 배열

문자 자료형 배열을 만들고 알파벳 대문자 A부터 Z까지 저장한 후 각 요소 값을 알파벳 문자와 정수 값(아스키 코드 값)으로 출력해 보겠습니다. 문자 자료형 배열은 char[]로 선언해야 합니다.

```java
ackage day04.array;

public class CharArray {
	public static void main(String[] args) {
		char[] alphabets = new char[26];
		char ch = 'A';
		
		for(int i = 0; i < alphabets.length; i++, ch++) {
			alphabets[i] = ch; // 아스키 값으로 각 요소에 저장
		}
		
		for(int i = 0; i < alphabets.length; i++) {
			System.out.println(alphabets[i] + "," + (int)alphabets[i]);
		}
	}
}

실행결과
A,65
B,66
C,67
D,68
E,69
F,70
G,71
H,72
I,73
J,74
K,75
L,76
M,77
N,78
O,79
P,80
Q,81
R,82
S,83
T,84
U,85
V,86
W,87
X,88
Y,89
Z,90
```
