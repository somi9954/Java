# 변수와 자료형

## 변수란?

- 공간에 담을수 있는 변하는 수
- 공간 = 메모리
- 공간(메모리)의 이름
- 공간 - 자료형
- 공간의 이름 - 변수명
- 자료형 : 데이터(=메모리 )

### 변수 선언하기

```java
자료형 변수명;
int 변수; ->자주 쓰임
```

```java
int number;
```

- number = 숫자;  -> 오른쪽 숫자 -> number 공간에 저장

### 변수 이름 정하기

1. 의미가 명확하게 이해되는 단어 ->max
2. 알파벳, 숫자, 일부 특수문자($, _)
3. 숫자는 앞에 올수 없다
4. 예약어
true, false, if, throw ..
5. 변수명을 구성하는 단어가 여러개인 경우
관례 
    1. 단어의 첫 글자는 대문자, 첫 단어의 첫글자는 소문자
    noOfStudent - **카멜 표기법**
    noOfOrder
    2. 단어와 단어 사이를 _로 표기
    no_of_student : **스네이크 표기법**

### 변수에 데이터 입력하기

```java
int num ;
num = 10;
```

### 변수 선언과 초기화

```java
int num = 10;
```

## 자료형

### 기본자료형

- 숫자를 담을수 있는 자료형
반도체 - 1, 0
1bit - 1,0으로 표현하는 최소 공간
1bit X 8 -> 1byte
1 - 부호비트(양수, 음수)

**정수**

```java
1byte  자료형 - byte  : -2^7 ~ 2^7 - 1 (-128~127)
												-> 0 ~ 255 / usigned byte : 양수 
 2byte 자료형 - short : -2^15 ~ 2^15 - 1
 (16bit)

 4byte 자료형 - int : -2^31 ~ 2^31 - 1
 (32bit)

 8byte 자료형 - long : -2^63 ~ 2^63 - 1
 (64bit)

```

**실수  - 소수점이 있는 숫자**

```java
 4byte 자료형 - float
 8byte 자료형 - double

```

**논리형 : 참, 거짓**

```java
1byte - boolean
true(참)
false(거짓)
```

**문자형**

```java
2~ 3byte - char
' ' : 문자 1개
예) '문자'
char ch = 'A';
```

<aside>
💡 아스키코드
숫자 - 문자

유니코드(2byte)
숫자 - 문자

</aside>

```java
char ch1 = 'A';
        System.out.println(ch1);
        System.out.println(ch1 + 1);
        System.out.println('A' + 'B');
```

```java
//출력값
A
66 -> 아스키 코드
131  -> 아스키코드
```

![image](https://github.com/somi9954/Java/assets/137499604/c032f382-de78-4db9-b61c-515fca0388eb)

char ch2 = '가';
        System.out.println(ch2 + 0);
				System.out.println('가' < '나');
```

```java
//출력값
44032
TRUE 
```

![image](https://github.com/somi9954/Java/assets/137499604/2c212dc6-0008-4fce-b0f6-24fde18445c2)


### 기본자료형 정리

![image](https://github.com/somi9954/Java/assets/137499604/ee216f12-6e9f-48ff-9ea2-98be23c067d7)


| 정수형 | 문자형 | 실수형 | 논리형 |
| --- | --- | --- | --- |
| 1바이트 | byte |  |  |
| 2바이트 | short | char |  |
| 4바이트 | int |  | float |
| 8바이트 | long |  | double |

## 참조자료형

- 다른 자원의 주소값을 가지고 있는 자료형
- JAVA에서 기본형(Primitive type)을 제외한 타입들이 모두 참조형(Reference type) 이다.
- 참조형(Reference type)은 JAVA에서 최상인 **java.lang.Object**클래스를 상속하는 모든 클래스들을 말한다.
- **클래스 타입(class type)**, **인터페이스 타입(interface type)**, **배열 타입(array type)**, **열거 타입(enum type)** 이 있다.

| String | 문자열을 저장하는 데 사용되는 클래스입니다. |
| --- | --- |
| ArrayList | 동적 배열을 나타내는 클래스입니다. |
| HashMap | 키-값 쌍을 저장하는 데 사용되는 클래스입니다. |
| HashSet | 고유한 요소를 저장하는 데 사용되는 클래스입니다. |
| LinkedList | 연결 리스트를 나타내는 클래스입니다. |
| Queue | 큐를 나타내는 인터페이스입니다. |
| Stack | 스택을 나타내는 클래스입니다. |

### Object

모든 `Class`와 `Enum`은 `Object` 클래스를 상속한다. 다시말해 Object는 모든 Class와 Enum의 일반화된 타입이라는 것이다. 여기서 주의할 점은 Interface는 Object를 상속하지 않는다는 사실이다. 이와 관련된 내용은 자바 api 문서 [Tree](https://docs.oracle.com/en/java/javase/16/docs/api/overview-tree.html)에 잘 드러나 있다.

> 자바 api 문서에는 제공하는 모든 Class, Interface, Enum 등의 상세 스펙을 정의하고 있다. 이 사이트는 자바를 깊이 이해하는데 많은 도움을 주므로 자주 방문하면 좋다. 다만 자바 버전에 따라 api구현이 상이하므로 주의해야 한다.
> 

### String

`String`은 기본 자료형이 아니라는 사실은 익히 잘 알려져 있다. String은 `char`의 배열로 구현된 참조 자료형이다.

> C/C++의 경우는 문자열을 사용하기 위해서 실제로 char형의 배열을 직접 사용한다.
> 

자바가 `C/C++`과 달리 `String`형을 따로 제공하는 이유는 문자열에 `유용한 메서드`를 제공하기 위해서이다. charAt, concat, equals, indexOf, split와 같은 메서드를 이용하면 문자열을 쉽게 조작할 수 있다.

### Array

`배열` 또한 마찬가지로 기본 자료형이 아니다. 이는 다음과 같은 간단한 코드를 통해서 테스트 해볼 수 있다.

```java
int[] array = new int[10];
System.out.println(array instanceof Object);
// true
```

모든 클래스는 Object의 상속 클래스이므로 위 코드를 통해 배열이 기본형이 아님을 알 수 있다. 만약 배열이 기본형이었다면 위와 같은 코드의 실행 결과 `false`가 나와야 한다.

### Wrapper 클래스

`Wrapper Class`는 기본 자료형을 감싼 클래스이다. 대표적으로 Byte, Short, Integer, Long, Float, Double, Character, Boolean이 있다. 이것을 사용하는 이유는 앞서 설명한 `String`을 사용하는 이유와도 동일하다. 기본 자료형을 `클래스`로 랩핑하면 얻을 수 있는 이점은 `유용한 메서드를 제공`할 수 있다는 점이다.

하지만 이보다 더 중요한 이유는 `제네릭(Generic)`에 있다. 제네릭에 사용되는 매개변수 `T`는 `Object` 자료형만 받을 수 있다. 이것은 다시 말해 클래스로 정의된 객체만을 전달받는다는 것이다. 다만 코드를 짜다보면 제네릭을 기본 자료형에 적용해야 하는 경우가 있다. 이러한 경우에는 `Wrapper Class`을 이용하면 문제가 해소된다.

> 제네릭을 통한 유연한 프로그래밍을 기본 자료형에도 적용할 수 있게 하기 위해 Wrapper Class를 제공한다고 생각하면 이해가 쉬울 것이다.
> 

### 기본자료형 vs 참조자료형

| 분류 | 기본 자료형(Primitive Data Type) | 참조 자료형(Reference Data Type) |
| --- | --- | --- |
| 종류 | 숫자, 문자, 논리값 등 | 클래스, 인터페이스, 배열, 열거 타입 등 |
| null 초기화 가능여부 | 초기화 불가능 | 초기화 가능 |
| 숫자간의 산술연산 가능여부 | 산술연산 가능 | 산술연산 불가능 |
| 제너릭 타입내 사용 가능여부 | 사용 불 가능 | 사용 가능 |
