## 항과 연산자

연산자

```java
10 + 20
```

- 항: 연산에 사용되는 값
1 -단항연산
2 -이항연산
3 -삼항연산

   조건식 ? 참일때 : 거짓일때

- 연산자: 연산에 사용되는 기호

### 대입연산자(=)

```java
int num1 = 10;
int num2 = 20;
int result = num1 + num2;
```

- 연산의 우선순위가 가장 낮다

### 2)부호연산자

- + ,-
- 부호 반전
음수-> 양수, 양수-> 음수

```java

public class Ex04 {
    public static void main(String[] args) {
        int num1 = 10;
        int num2 = -num1; // -10
        System.out.println(num2);

        int num3 = -num2; // 10
        System.out.println(num3);
    }
}
출력값
-10
10
```

### 산술연산자

- +,-,*,/,%
- ,/,% >,+,-
- % : 균등배분 - 나머지는 나누는 수보다 작고, 0~나누는수 1
- + : 수치 → 숫자의 덧셈

            문자 → 문자열 배열

- (...) : 우선순위 강제 적용
- 참고) 문자열 : 문자가 여러개 있는 형태 - 단어, 문자 , ⇒ “문구…”

               문자열 + 다른자료형 : 문자열 기준으로 결합

               String 변수명 = “문자열….”;

                char ch = ‘a’; //문자 1개

```java
public class Ex05 {
    public static void main(String[] args) {
        System.out.println(1 % 3);
        System.out.println(2 % 3);
        System.out.println(3 % 3);
        System.out.println(4 % 3);
        System.out.println(5 % 3);
        System.out.println(6 % 3);
        System.out.println(7 % 3);
        System.out.println(8 % 3);
        System.out.println(9 % 3);

    }
}

**출력값
1
2
0
1
2
0
1
2
0
```

- 문자열 + 다른자료형 : 문자열 기준으로 결합 ⇒ 연산자 오버로드

```java
public class Ex06 {
    public static void main(String[] args) {
        String str1 = "ABC";
        String str2 = "DEF";
        boolean result = true;
        int num = 100;
        System.out.println(str1 + str2 + result + num );
    }
}
```

### 증가감소 연산자

- ++: 1씩 증가
- --: 1씩 감소

```java
num = num + 1
num++;
++num;

int num = 10;
int num2 = num++;
	num = 11
	num2 = 10

int num = 10;
int num2 = ++num;
	num = 11;
	num2 = 11;
```

### 비교 연산자(관계)

- 논리값 (참, 거짓)
- > , <, >=, <=, ==, !=
- 연산의 결과 : boolean : true, false → 논리값 → 판별/ 조건식

### 논리 연산자

- AND연산 : && - 교집합
참 && 참 -> 참
- 비교 연산의 값이 출력된다.
- OR연산 : || -합집합
참|| 참 -> 참
참|| 거짓 -> 참
거짓||참-> 참
    
    거짓||거짓-> 거짓
    
- NOT연산: ! -참 -> 거짓, 거짓-> 참
- 연산의 결과 논리값(boolean - true, false)
- 비교 연산이 논리 연산보다 우선순위가 낮다!
    
    ||연산자 -> 하나라도 true 이면 true
    && 연산자  -> 모두 true 이면 true
    
 ![image](https://github.com/somi9954/Java/assets/137499604/b2ce1a0b-7970-4ee8-8e6b-817dd3d05ed7)

    

참고) 단락회로 평가

- 참 거짓 판별 → 앞에 식이 참이면 더이상 체크하지 않고 true로 반환값이 나온다.

```java
public static void main(String[] args) {

        int num1 = 10;
        boolean result = num1++ > 9 || (num1 = num1 + 10) > 30;
        System.out.println(result);

        System.out.println(num1);
    }
}
```

### 복합 대입 연산자(단항)

- 산술연산자(+, -, *, /, %) + 대입(=)

```java
int num1 = 10;
num = num + 2;  => num += 2;
num = num * 2;  => num *= 2;

num1 *=3 // num1 = num1*3
```

### 조건 연산자(삼항 조건 연산자)

조건식 ? 참일때 : 거짓일때
(1항)       2항        3항

```java
public class EX03_16 {
	public static void main(String[] args) {
		int num = (7 > 1) ? 1 : 2;
		System.out.println(num);
	}
}
출력값 
1
```

### 연산자 우선순위

- = (대입) <        .... 논리 < 비교 ...      <       단항 ..  <  (  )
- 같은 우선 순위의 연산자
    - 왼쪽에서 오른쪽으로 처리가 기본
    - 예외사항) 대입연산자, 증감, 부호, '!', 형변환시
- 괄호는 가장 최우선 순위
- 연산의 종류
    
![image](https://github.com/somi9954/Java/assets/137499604/506ad68e-3bf1-4a13-816b-ed4303193d35)
