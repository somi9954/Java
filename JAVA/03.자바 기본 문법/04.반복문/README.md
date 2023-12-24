## 반복문

### while문

- 반복 조건이 *true*이면 반복, *false*이면 반복 종료
- 반복 조건이 없으면 컴파일 오류 (*for* 문과의 차이점)
- 조건식에 맞지 않으면 수행않음 (*do-while* 문과의 차이점)

```java
while (조건식 ) {
 // 조건식이 참일때 반복 수행되는 코드
}
```

```java
public class Ex13 {
    public static void main(String[] args) {
        int num = 1, total = 0;

        while(num <= 100) {  //조건 먼저 실행  num <1 인경우 실행
            total += num;    //하지 못함
            num++;
        }
        System.out.println(total);
    }
}
출력값
5050
```

### do-while문

- 무조건 최소 한번의 명령이 실행
- 반복 조건이 *true*이면 반복, *false*이면 반복 종료
- 반복 조건이 없으면 컴파일 오류
- 무한반복에 빠지지않도록 종료조건을 설정해주어야함

```java
do {

// 조건식이 참일때 반복 수행되는 코드
// 조건식이 거짓이더라도 일단 한번은 수행

} while(조건식);
```

```java
int i = 0;
do {
System.out.println(i);
i++;
} while (i < 10)
```

```java
public class Ex14 {
    public static void main(String[] args) {
        int num = 1 , total = 0;

        do {
            total += num;  // 코드 먼저 실행  num<1 이여도 한번은 실행
            num++;          
        }while (num <= 100); 
        System.out.println(total);
    }
}
출력값
5050
```

### for문

```java
for( 초기화식 ; 조건식; 증감식){
   // 조건식이 참일때 반복 수행되는 코드
}

```

![image](https://github.com/somi9954/Java/assets/137499604/b4bcc1a7-f3f9-4617-b1ed-dfc4e9be24d6)


```java
package exam01;

public class Ex15 {
    public static void main(String[] args) {
        int total = 0 ;
        for (int num = 1; num <= 100; num++) {
            total += num;
        }
        System.out.println(total);
    }
}

출력값 
5050
```

- 반복 중단 : break ;

```java
public class Ex15 {
    public static void main(String[] args) {
        int total = 0 ;
        for (int num = 1; num <= 100; num++) {
            total += num;

            if (num == 50) {
                break;
            }
        }
        System.out.println(total);
    }
}

출력값
1275
```

- 1,3,5,7,9,11,13 … // 2n+ 1 → 2로 나누었을때 나머지가 1인 경우 홀수

```java
public class Ex15 {
    public static void main(String[] args) {
        int total = 0 ;
        for (int num = 1; num <= 100; num++) {
            if (num % 2 == 1) { //홀수 
                total += num;
            }

           /* if (num == 50) {
                break;
            }*/

        }
        System.out.println(total);
    }
}

출력값 
2500
```

- continue : 현재 반복을 중단, 새로 시작

```java
public class Ex15 { 
    public static void main(String[] args) {
        int total = 0 ;
        for (int num = 1; num <= 100; num++) {
            if (num % 2 == 0) {  // 짝수
               continue;
            }
            total += num;

           /* if (num == 50) {
                break;
            }*/

        }
        System.out.println(total);
    }
}
```

- for 문 변수명 관례  횟수, 순서 (index)
- 관례적으로 초기화식 변수명으로 ‘i’ 부터 시작하고 다음 알파벳부터 순서대로 사용한다. (i, j,k ….)

### 중첩반복문

- 반복문 안에 반복문 ( for문 예시)

```java
public class Ex16 {
    public static void main(String[] args) {
        for (int i = 1 ; i <= 9; i++) {
            System.out.println("------------" + i + "단 ----------");
            for (int j = 1; j <= 9 ; j++) {
                System.out.println(i + "X" + j + " = " + (i*j));
            }
        }
    }
}

출력값
------------1단 ----------
1X1 = 1
1X2 = 2
1X3 = 3
1X4 = 4
1X5 = 5
1X6 = 6
1X7 = 7
1X8 = 8
1X9 = 9
------------2단 ----------
2X1 = 2
2X2 = 4
2X3 = 6
2X4 = 8
2X5 = 10
2X6 = 12
2X7 = 14
2X8 = 16
2X9 = 18
...
```
