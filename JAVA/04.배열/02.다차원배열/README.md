# 다차원배열

- 2차원 이상의 배열 다차원의 배열도 선언해서 사용할 수 있다. 평면이나 공간 개념을 구현하는데 사용한다.
- 2차원 배열은 [행]과[열]로 이뤄졌으며 평면으로 되어 있다.
- 3차원 배열은 입체적이다.

## 이차원 배열 선언

일차원 배열에서 [ ] 가 한개 더 추가된다.

자바에서 배열을 선언하는 방법은 다음과 같습니다.

```java
자료형[][] 배열변수명;
자료형 배열변수명[][];
```

예를 들어 배열은 다음과 같이 선언합니다.

```java
int intArray[][];
char charArray[][];
String name[][];
```

또는  다음과 같이 선언합니다.

```java
int[][] intArray;
char[][] charArray;
String[][] name;
```

### 배열 생성

 배열의 객체를 생성하려면 목록의 값을 이용하거나 New 연산자를 사용한다.

```java
자료형 배열변수명[행][열] = new 자료형[공간의 갯수][공간의 갯수];
```

자바에서 배열을 생성하는 방법은 다음과 같습니다.

```java
int[][] Array = new int[10][];
int[][] nums = new int[2][3];
int[][] score = new int[3][];
char[][] charArray = new char[5][];
```

![image](https://github.com/somi9954/Java/assets/137499604/5023a3d0-f157-4bc2-ac0e-6e48cdd4fa67)

int[ ][ ] nums = new int[2], [3];

<aside>
💡 2차원 배열은 다양한 방식으로 선언할 수 있는데 열을 지정하지 않고 선언이 가능하다.

</aside>

### 배열의 생성 및 초기화 출력

배열의 생성 및 초기화는 다음과 같습니다.

```java
public class _04_MutiArrayLoop {
    public static void main(String[] args) {
        String[][] seats = new String[][]{
                {"A1", "A2", "A3", "A4", "A5"},
                {"B1", "B2", "B3", "B4", "B5"},
                {"C1", "C2", "C3", "C4", "C5"},
        };

        for (int i = 0; i <seats.length; i++) { //세로 기준(행)
            for (int j = 0; j < seats[i].length;; j++) { //가로기준 (열)
                System.out.print(seats[i][j] + " ");
            }
            System.out.println();

        }
```

![image](https://github.com/somi9954/Java/assets/137499604/369b3cd8-ec91-4f36-8ec5-5b19e5961596)


• 중첩 for문은 배열 인덱스용으로 i, j 두 변수를 사용하는데 i는 행을. j는 열을 가리킵니다. 전체 배열 길이인 seats.length는 행의 개수를 각 행의 길이 seats[i].length는 열의 개수를 나타냅니다.

```java
public class _04_MutiArrayLoop {
    public static void main(String[] args) {
        String[][] seats = new String[][]{
                {"A1", "A2", "A3", "A4", "A5"},
                {"B1", "B2", "B3", "B4", "B5"},
                {"C1", "C2", "C3", "C4", "C5"},
        };
			System.out.println(Arrays.deepToString(seats));
		}
}
```

![image](https://github.com/somi9954/Java/assets/137499604/50c05cdd-7846-4884-92b0-1a637b79f0f7)

이 외에 deepToString() 메서드를 이용해 출력할 수 있다.
