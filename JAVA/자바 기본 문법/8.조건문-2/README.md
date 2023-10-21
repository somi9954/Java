### 선택문 - switch

- switch/case 문은 if 문과 비슷하지만 좀 더 일정한 형식이 있는 조건·판단문이다.
- switch/case 문의 구조는 다음과 같다.

```java
switch (키워드) {
case 값1:
키워드가 값1과 일치할때 수행되는 코드...
break; - 실행 중단 => 구문을 끝내고 완전히 나가는 역할 
case 값2:
키워드가 값2와 일치할때 수행되는 코드....

 break; => 중요 
 .....
 default:
	키워드가 모든 케이스에 매칭 X -> 실행되는 코드

```

- 입력 변수의 값과 일치하는 case 입력값(입력값1, 입력값2, …)이 있다면 해당 case 문에 속한 문장들이 실행된다. case 문마다 break라는 문장이 있는데 해당 case 문을 실행한 뒤 switch 문을 빠져나가기 위한 것이다.
- **break;** 가 없으면 모든 값이 다 출력되기 때문에 break가 중요하다.
- **default** 는 위의 case가 없을때 값을 출력하기 위한 키워드이며 생략은 가능하나 아무값이 발생되지 않기 위해 막는 키워드이다.
- 키워드는 **정수**로만 가능하다.

```java
public class Ex12 {
    public static void main(String[] args) {
        int rank = 4;
        switch (rank) {
            case 1:
            System.out.println("금메달");
            break;
            case 2:
                System.out.println("은메달");
                break;
            case 3 :
                System.out.println("동메달");
                break;
            default:
                System.out.println("입상!");
        }
    }
}
```

```java
public class EX04_12 {
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.println("원하는 숫자를 입력하세요. (1~5)");
		
		int num = sc.nextInt( );
		switch(num) {
			case 5:
				System.out.println("5를 입력하였습니다.");
				break;
			case 4:
				System.out.println("4를 입력하였습니다.");
				break;
			case 3:
				System.out.println("3을 입력하였습니다.");
				break;
			case 2:
				System.out.println("2를 입력하였습니다.");
				break;
			case 1:
				System.out.println("1을 입력하였습니다.");
				break;
			default:
				System.out.println("1~5까지의 숫자를 입력하세요.");
		}
	}
}
출력값 
원하는 숫자를 입력하세요 (1~5)
3
3을 입력하였습니다.
```

- char도 문자열에 맞는 정수이기  때문에 적용이 가능하다.

```java
public class Ex12 {
    public static void main(String[] args) {
        //int rank = 4;
        char rank = 'A';
        switch (rank) {
            case 'A':
            System.out.println("금메달");
            break;
            case 'B':
                System.out.println("은메달");
                break;
            case 'c':
                System.out.println("동메달");
                break;
            default:
                System.out.println("입상!");
        }
    }
}
출력값
금메달
```
