### 상수와 리터럴

- 변하지 않는 수
- final 예약어 변수명 앞에 추가
- final : 최종적, 마지막
- 이름 명명 관례  → 대문자, 단어와 단어 사이 ‘_ ‘로 구분

```java
final int Max_NUMBER = 10;
```

- final 이기 때문에 변경하지 못한다.

![image](https://github.com/somi9954/Java/assets/137499604/86c97f5a-6987-48b2-906a-9c5f2427caf3)


리터럴(literal)

- 리터럴 상수
- 재료가 되는 수(문자, 숫자, 논리값)
- 같은 재료 → 하나만 생성 (상수)

```java
int a = 10 ;
int b = 10;
```

![image](https://github.com/somi9954/Java/assets/137499604/ced1a020-9d30-4f49-b745-4081b43eb7ae)


- 모든 정수를 처음에는 int 인식
    
    ```java
    long num = 1000000000000L; //  int -> long
            byte num2 = 100; // int 100 -> byte 100
            int num3 = 100; //효율적
    ```
    
- 모든 실수를 처음에는 double로 인식

```java
double num4 = 100.1234; //효율적
float num5 = 100.1234F;  //double -> float
```
![image](https://github.com/somi9954/Java/assets/137499604/01efba78-d0fd-478e-9a2b-ea97cf971464)

