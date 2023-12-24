# 향상된 for문 (= for each문)

- JDK1.5부터 제공되는 향상된 for문(enhanced for loop)은 배열의 처음부터 끝까지 모든 요소를 참조할 때 사용하는 편리한 반복문 입니다.
- 향상된 for문은 배열 요소 값을 순서대로 하나씩 가져와서 변수에 대입합니다.
- 따로 초기화와 종료 조건이 없기 때문에 모든 **배열의 시작 요소부터 끝 요소까지 실행**합니다.

### 기본구조

```java
for(각각요소 : 배열(컬렉션)) {
         반복 실행문;
}
```

![image](https://github.com/somi9954/Java/assets/137499604/305ae21a-3917-4305-8bed-79d0bddf2e3b)


for문을 실행할 반복 대상이 있으면 자료형은 반복 대상이 지닌 자료형과 같은 타입으로 지정해야 한다. 반복 대상의 요소를 하나씩 대입하면서 진행하고, 반복 대상의 길이만큼 꺼내어 반복한다.

```java

public class ex03 {
    public static void main(String[] args) {

        int[][] arr = { { 1, 2, 3 }, { 4, 5, 6 } };

        for (int[] lang : arr) {
            for (int i : lang) {
                System.out.println(i);
            }
            System.out.println();
        }
        
    }
}
```

![image](https://github.com/somi9954/Java/assets/137499604/6640cb8e-59d2-448e-9b47-7166445bfd21)



```java
public class ex03 {
    public static void main(String[] args) {

        int[] score = {90, 92, 93};

        int sum = 0;
        double avg = 0;

        for (int val : score) {
            sum += val;
        }

        avg = (double) sum / 3;
        System.out.println("총점 : " + sum + ", 평균 : " + avg);
    }
}
```

![image](https://github.com/somi9954/Java/assets/137499604/d8290b00-1607-4cd7-84d1-4d73cbebc50f)
