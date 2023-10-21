## 형변환

- 자료형간 변환

### 묵시적 형변환

- 자동 형변환
- 작은 자료형 -> 큰 자료형 변환할 때 사용
- 정수(덜 정밀한 숫자) -> 실수(더 정밀한 숫자)으로 변환할 때 사용
- 연산 중 자동 형변환 : 연산은 같은 자료형만 가능 -> 연산을 위해서 자동 형변환

![image](https://github.com/somi9954/Java/assets/137499604/e4b674de-7551-492d-a121-e19be20b11b1)

```java
public static void main(String[] args) {
        int num1 = 100;
        long num2 = 200L;
        long num3 = num1 + num2; // int num1 -> long num1

        int num4 = 10;
        double num5 = 2.5;
        double num6 = num4 * num5; // num4 -> double num4
        System.out.println(num6);
    }

출력값 
25.0
```

```java
public class EX02_26 {
	public static void main(String[] args) {
		int i = 100;
		char c = 'a';
		int j = c; // char형에서 int형으로 자동 변환.
		double d = i; // int형에서 double형으로 자동 변환.
		
		System.out.println("int형 변수 j의 값 : " + j);
		System.out.println("double형 변수 d의 값 : " + d);
	}
}
출력값 
int형 변수 j의 값 : 97
double형 변수 d의 값 : 100.0
```

### 명시적 형변환

- 데이터의 유실이 발생할 가능성이 있는 경우 - 자동 형변환 X

       큰자료형 → 작은 자료형

        실수 → 정수 

- 명시적으로 형변환 의사 표현
    
    (자료형)값(변수)
    

```java
public class Ex02 {
    public static void main(String[] args) {
        int num1 = 100;
        byte num2 = (byte) num1; // 강제형변환 데이터의 유실이 생길 수 있다.
        System.out.println(num2);

        double num3 = 100.123;
        int num4 = (int) num3;
        System.out.println(num4);
    }
}
출력값 
100
100
```

```java
public class EX02_28 {
	public static void main(String[] args) {
		
		// double형 → f loat형 강제 형 변환(f loat형 범위 내 값)
		double d1 = 1.1234;
		float f1 = (float) d1;
		System.out.println("[double -> float] d1의 값 :" + d1 + ", f1의 값 :" + f1);
		
		// double형 → f loat형 강제 형 변환(f loat형 최소값보다 작은 경우)
		double d2 = 1.0e-50;
		float f2 = (float) d2;
		System.out.println("[double -> float] d2의 값 :" + d2 + ", f2의 값 :" + f2);
		
		// double형 → f loat형 강제 형 변환(f loat형 최대값보다 큰 경우)
		double d3 = 1.0e100;
		float f3 = (float) d3;
		System.out.println("[double -> float] d3의 값 :" + d3 + ", f3의 값 :" + f3);
		
		// double형과 f loat형의 정밀도 차이
		double d4 = 9.123456789;
		float f4 = (float) d4;
		System.out.println("[정밀도 차이] d4의 값 :" + d4 + ", f4의 값 :" + f4);
	}
}

출력값 
[double -> float] d1의 값 : 1.1234, f1의 값 1.1234
[double -> float] d2의 값: 1.0E-50, f2의 값 : 0.0
[double -> float] d3의 값 : 1.0E100, f3의 값 : Infinity
[정밀도 차이] d4의 값 : 9.123456789, f4의 값:9.123457
```

### 기본자료형의 기본값

- 정수형 : 0
- 실수형 : 0.0
- 논리형 : false

```java
public class Ex02 {
    static int num5;
    static double num6;
    static boolean result;

public static void main(String[] args) {
        System.out.println(num5);
        System.out.println(num6);
        System.out.println(result);
}

출력값 
0
0.0 
false
```
