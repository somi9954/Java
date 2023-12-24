## 메서드란?

- 클래스 안에서 특정 기능을 수행하기 위해 코드들을 따로 하나의 블록으로 묶어 놓은 집합을 말한다.
- 멤버(member)로 속성을 표현하는 필드(field)와 기능을 표현하는 메서드(method)를 가집니다.
- **클래스, 구조체, 열거형에 포함되어있는 함수(functtion)이다.**
- 함수(function)의 종류이다.

### 함수란?

- 하나의 기능을 수행하는 일련의 코드
- 함수는 어떤 기능을 수행하도록 미리 구현해 놓고 필요할 때마다 호출**하여 사용할 수 있습니다.**
- 함수는 특정 작업을 수행하는 "**코드조각**"이다. 전역, 지역이던 "**독립된 기능**"을 수행하는 단위

### 함수의 입력과 반환

- 함수는 이름이 있고, 입력된 값과 결과 값을 갖습니다.
- 두 수를 더하는 함수를 예로 들면 두 수를 입력받아서 '더하기 함수'를 거치면 두 수의 합을 반환합니다.

![image](https://github.com/somi9954/Java/assets/137499604/2c89247f-21e9-403e-82ab-2270f42a8dcb)


- 함수에 이름을 붙일 때는 의미를 알 수 있는 단어를 사용하는 것이 좋습니다. 더하는 함수 이므로 **add**라고 이름을 짓습니다.
- 더하는 두 수는 각각 num1, num2라고 정합니다.
- num1, num2와 같이 함수의 입력을 받는 변수를 **매개변수**라고 합니다.
- 두 수를 더한 결과 값을 result 변수에 저장하여 돌려 줍니다. 이를 '**결과를 반환한다**'고 합니다.
- 이렇게 함수를 수행한 후, 결과로 되돌려 주는 값인 result를 **반환값**이라고 부릅니다.

### 함수 정의하기

함수가 하는 일을 코드로 구현하는 것을 **함수를 정의 한다** 라고 합니다.

![image](https://github.com/somi9954/Java/assets/137499604/3afa5377-88a6-451d-9237-ed172b52c8bc)

### 함수이름

- 함수 이름은 add라고 썼습니다.
- (1) 위치가 함수 이름을 적는 부분입니다.
- 함수 이름은 변수 이름처럼 프로그래머가 임의로 만들면 되는데, 함수 기능과 관련있게 만들어야 나중에 호출하거나 이해하기 좋습니다.

### 매개변수

- add 함수는 두 값을 더하는 일을 합니다.
- 덧셈을 수행하기 위해서는 먼저 함수에 두 값이 입력되어야 합니다.
- 함수는 넘겨받은 값으로 덧셈을 수행합니다. 이렇게 함수 내부에서 사용할 괄호 안의 변수를 **매개변수**라고 합니다.
- (2) num1과 num2가 매개변수 입니다.
- 경우에 따라서는 **매개변수**가 필요없는 함수도 있습니다.

```java
int getTenTotal() {
	int i;
	int total = 0;
	for(i = 1; i <= 10; i++) {
		total += i;
	}
	
	return total;  // 1부터 10까지 더한 값을 반환 
}
```

![image](https://github.com/somi9954/Java/assets/137499604/3f186109-a165-4df2-89b5-45e189cdec90)

위 방정식을 코드로 정리하게 되면 다음과 같이 정리된다.

```java
package exam01;

public class Ex02 {
    public static void main(String[] args) {
    int result = func(3);
        System.out.println(result);
    }

    static int func(int x) {
        int y = x * 2 + 1;

        return y;
    }
}

호출값
7
```

### return 예약어와 반환형

- add()함수를 수행한 후 결과 값은 변수 result에 저장됩니다.
- result에 저장된 결과 값은 함수를 호출했을 때 반환되는 값이므로 **반환값**이라고 부릅니다.
- '**이 함수의 결과 값을 반환 합니다.**를 뜻하는 예약어가 **return**입니다.
- (3) return 예약어를 사용하여 result 값을 반환하는 것 입니다.
- 반환 값의 자료형을 반환형이라고 하는데 (4) 위치에 써 줍니다.
- 이 함수에서 변수 **result**의 반환형은 정수형이므로 (4)위치에 **int**라고 적습니다.
- 경우에 따라서는 **반환값이 없는 함수**도 있습니다.
- 반환값이 없다고 해서 반환형을 쓰는 (4)위치를 비워두면 오류가 발생합니다. 이 때에는 (4)위치에 **void**라고 씁니다.
- **void**는 비어있다는 의미로 '**반환할 값이 없다**'는 뜻의 예약어입니다.

```java
void printGreeting(String name) {
	System.out.println(name + "님 안녕하세요");
	return; // 반환값 없음 (생략 가능)
}
```

- return 예약어는 함수 수향을 끝내고 프로그램 흐름 중에서 호출한 곳으로 다시 되돌아갈 때도 사용할 수 있습니다.

```java
 void divide(int num1, int num2) {
	if (num2 == 0) {
		System.out.println("나누는 수는 0이 될 수 없습니다.");
		return; // 함수 수행 종료
	} else {
		int result = num1 / num2;
		System.out.println(num1 + "/" + num2 + "=" + result + "입니다.");
	}
 }
```

- 나누는 수가 0이라면 함수 수행을 하면 안되므로 함수 수향을 종료하는 예약어 return을 사용합니다.
- **함수 수행을 종료하는 목적**이므로 return 뒤에 반환값을 적지 않아도 됩니다.

### 메서드를 사용하는 이유

메서드를 구현함으로써 같은 내용의 코드를 반복적으로 사용하는 것을 피할 수 있다.  즉 반복되는 문장들을 묶어서 메서드로 작성해 놓으면 필요할 때마다 재사용이 가능하며 중복된 코드를 제거할 수 있다.

**메서드 선언 방법은 다음과 같습니다.**

```java
//  선      언       부                
접근 제한자 반환타입 메서드이름() {     실
//기능을 수행할 코드                    행
                                       영
}                                      역
```

![image](https://github.com/somi9954/Java/assets/137499604/cebb196d-f97f-49d7-afd9-dd79acfdd443)


메서드의 선언부는 후에 변경사항이 발생하지 않도록 신중하게 작성하여야 한다. 메서드의 선언부를 변경하게 되면 그 메서드가 호출되는 모든 곳이 함께 변경되어야 하기 때문이다.

**매개변수** :  특정 기능을 수행할 때 사용할 인수를 매개변수라고 한다.  즉 메서드가 수행할때 필요하는 값을 제공받기 위한 것이다. 메서드를 정의할때 ( ) 소괄호 안 형태로 되어있다. 선언할 수 있는 매개변수는 제한이 없으나 입력값의 개수가 많은 경우에는 배열이나  참조변수를 사용하면 된다. 만약 입력값이 없을 경우에는 소괄호안에 값을 넣지 않으면 된다. 변수선언과 달리 두 변수의 타입이 같아도 변수의 타입을 생략할 수 없다.

```java
//매개변수를 배열로 받는 메서드의 정의
package section08;

public class Calc {
	void sum(int num1, int num2) {
		System.out.println("두 수의 합은 " + (num1 + num2) + "입니다.");
	}
}
```

```java
package section08;

public class EX08_13 {
	public static void main(String[] args) {
		int nums[] = {100, 200}; // 배열 생성
		Calc calc = new Calc(); // Calc 객체 생성
		calc.sum(nums); // calc 인스턴스의 sum 메서드 호출
	}
}

출력값 
두 수의 합은 300입니다
```

**반환타입**:  메서드의 작업수행 결과(출력)인 반환값(return value)의 타입을 적는다. 반환값이 없는 경우는 void 를 적어야한다.

**return문**  :메서드를 호출할 때 매개변수를 전달해 준 것처럼, 필요에 따라 메서드로부터 실행한 결과값을 되돌려 받을수도 있다. 이것을 리턴값(return value)라고 한다. 메서드로 입력(매개변수)는 여러 개 일 수 있어도 출력(반환값)

 

```java
접근 제한자 반환타입 메서드 이름() {
//기능을 수행할 코드들 

return결과값;
}
```

자료형의 크기에 따라 실제로 던질 리턴값보다 작은 자료형으로 자동형변환이 되어 반환하는것도 가능하다.

> void 는 '빈 공간, 아무것도 없다'라는 의미를 가진 단어이다.
함수가 아무것도 반환하지 않을 때 사용한다.
즉, return 이 없을 때 사용한다.
아무것도 반환하지 않는 함수는 void 타입을 가지고, void 타입인 함수는 undefined를 리턴한다.
> 

```java
package section08;

public class MidTerm {
	public int score(int[] scores) {
		int result = 0;
		for(int i = 0; i < scores.length; i++) {
			result += scores[i];
		}
		
		return result;
	}
}
```

```java
package section08;

public class EX08_17 {
	public static void main(String[ ] args) {
		int[ ] studentA = {97, 53};
		int[ ] studentB = {95, 66};
		
		MidTerm mid = new MidTerm(); // MidTerm 객체 생성
		int sumA = mid.score(studentA); // 메서드를 호출한 결과값을 sumA에 저장
		int sumB = mid.score(studentB); // 메서드를 호출한 결과값을 sumB에 저장
		
		if(sumA > sumB) {
			System.out.println("A학생의 중간고사 총점이 더 높습니다.");
		} else if(sumA < sumB) {
			System.out.println("B학생의 중간고사 총점이 더 높습니다.");
		} else { // sumA == sumB
			System.out.println("두 학생의 중간고사 총점이 같습니다.");
		}
	}
}

반환값
B학생의 중간고사 총점이 더 높습니다.
```

**지역변수** : 메서드 내에 선언된 변수들은 그 메서드 내에서만 사용 할 수 있으므로 서로 다른 메서드라면 같은 이름의 변수를 선언해도 된다. 이처럼 메서드 내에 선언된 변수를 지역 변수라고 한다.

### 메서드 호출

```java
package section08;

public class Jogger {
	void run() {
		System.out.println("run run run!");
	}
}
```

```java
package section08;

public class EX08_03 {
	public static void main(String[] args) {
		Jogger jogger = new Jogger(); // 객체 생성
		jogger.run(); // jogger 인스턴스의 run( ) 메서드 호출
	}
}
출력값 
run run run!
```

### 호출과 스택

호출스택은 메서드의 작업에 필요한 메모리 공간을 제공한다. 메서드가 호출하게 되면 호출스택에 호출된 메서드를 위한 메모리가 할당되며, 이 메모리는 메서드가 작업을 수행하는 동안 지역변수(매개변수 포함)들과 연산의 중간 결과등을 저장하는데 사용된다. 메서드가 작업을 마치면  할당되었던 메모리 공간은 반환되어 비워진다.

```java
class Ex {
public static void main(String[] args) {
        int num1 = 10;
        int num2 = 20;
			  int num3 = num1 + num2;
        int result = add(num1, num2);
        System.out.println(num3);
				System.out.println(result);
    }

    static int add(int num1, int num2) {
        int num3 = num1 + num2;

        return num3;
    }
}

```

![image](https://github.com/somi9954/Java/assets/137499604/f0fc50bf-52bc-4648-a83c-4fb8527aeb61)


![image](https://github.com/somi9954/Java/assets/137499604/336c5787-dfa7-42e5-89ee-dcfb107df4a9)


위의 코드를 실행 시키면  JVM에 의해서 main 메서드가 호출됨으로써 프로그램이 실행된다. 이 때 호출 스택에서는 main메서드를 위한 메모리공간이 할당되고 main메서드의 코드가 수행되기 시작한다.

main메서드에서 add() 를 호출한 상태이다. 아직 main메서드가 끝난것은 아니므로 main메서드는 호출스택에 대기상태로 남아있고, add()의 수행이 시작된다.  add()메서드를 통해 ‘30’가 출력된다.

add메서드의 수행이 완료되어 호출스택에서 사라지고 자신을 호출한 main메서드로 돌아간다.  대기중이던 main 메서드는 add를 호출한 후 부터 수행을 재개한다.

main 메서드에서도 result를 호출 하게 된 후  더이상 수행할 코드가 없으므로 종료되어 호출스택은 완전히 비워지게 되고 프로그램은 종료된다.

### 메서드 오버로딩(****method overloading)****

: 같은 이름을 갖고 있지만, 서로 다른 매개변수 형식을 가지고 있는 메서드를 여러 개 정의하는 것이다.

메소드 오버로딩 구분 요건은 아래와 같다.

- 메소드 이름이 같아야 한다.
- 매개변수의 개수, 타입 또는 순서가 달라야 한다.
- 반환 타입은 관계 없다.

**ex) 매개변수 개수가 다른 경우의 메소드 오버로딩**

![image](https://github.com/somi9954/Java/assets/137499604/6838d0e9-df11-4593-9fb8-f67199e2277f)
출처 : https://developer-yeony.tistory.com/94

매개변수 개수가 다르다.

![image](https://github.com/somi9954/Java/assets/137499604/3df93cfd-be48-4e5c-afa3-4ddb11c591fd)


메소드이름이 같아도 인자의 개수가 다르기 때문에 알아서 인식된다.

**ex) 매개변수 타입이 다른 경우의 메소드 오버로딩**

![image](https://github.com/somi9954/Java/assets/137499604/a8169ee1-eabc-4de4-a31b-738c132530dd)
출처 : https://developer-yeony.tistory.com/94

매개변수 자료형 타입이 다르다.

![image](https://github.com/somi9954/Java/assets/137499604/863743d8-e263-441c-b913-ce8554f85226)
출처 : https://developer-yeony.tistory.com/94

메소드이름이 같아도 인자의 자료형 타입이 다르기 때문에 알아서 인식된다.

**ex) 매개변수 순서가 다른 경우의 메소드 오버로딩**

![image](https://github.com/somi9954/Java/assets/137499604/4ccfb8b4-5c7a-45dd-8816-77a16a8b76d4)
출처 : https://developer-yeony.tistory.com/94

매개변수 순서가 다르다.

![image](https://github.com/somi9954/Java/assets/137499604/2911898c-54fe-4b65-8b71-b4cece2f25d5)
출처 : https://developer-yeony.tistory.com/94

메소드이름이 같아도 인자의 순서가 다르기 때문에 알아서 인식된다.

**ex) 반환타입은 오버로딩 구현하는데 아무런 영향을 주지 않아 컴파일 에러가 발생한다.**

![image](https://github.com/somi9954/Java/assets/137499604/d03a2a6e-234c-4894-aa61-fce500f08b77)
출처 : https://developer-yeony.tistory.com/94

리턴타입을 다르게 한 오버로딩 문법은 적용 안된다.

자**바 가변인자(Varargs, Variable Argument List)**

자바 1.5에서 추가된 가변인자 문법이다. **"자료형타입 ... 배열명"** 형식으로 이 문법은 매개변수 개수가 다른 메소드가 오버로딩 된 경우 그 인자 개수만큼 가변인자로 받아서 배열로 처리하면 한 개의 메소드만 정의하면 된다.

가변인자 문법을 사용하지 않으면, 인자개수만큼 중복 메소드명을 오버로딩 시켜야한다. 그만큼 불필요한 코드라인이 늘어나므로, 가변인자를 이용해 한 개의 메소드만 정의하면 코드줄 수가 줄어든다.

![image](https://github.com/somi9954/Java/assets/137499604/c8b9eee2-ee12-4f78-acb0-f88c362c9c36)
출처 : https://developer-yeony.tistory.com/94

가변인자를 이용해 메소드를 생성.

![image](https://github.com/somi9954/Java/assets/137499604/ba549b50-a767-4755-bf74-7414f93cbc9a)
출처 : https://developer-yeony.tistory.com/94

메인 메소드에서 p메소드 호출.

![image](https://github.com/somi9954/Java/assets/137499604/0547a36c-6567-4067-89bc-686d7777eab5)
출처 : https://developer-yeony.tistory.com/94

출력 화면

**오버로딩의 장점**

하나의 이름으로 정의할 수 있다면 기억하기도 쉽고 메서드의 이름도 절약이 가능해 오류를 줄일 수 있다.

```java
void println()

void printlnBoolean (boolean x)

void printlnChar (char x)

void printlnDouble (double x)

void printlnString (String x)
```

매개변수에 따라 메서드의 이름을 다르게 해야 한다면 "낭비"이다.

### 용어 정리

| 용어 | 설명 |
| --- | --- |
| 객체 | 객체 지향 프로그램의 대상, 생성된 인스턴스 |
| 클래스 | 객체를 프로그래밍 하기 위해 코드로 만든 상태 |
| 인스턴스 | 클래스가 메모리에 생성된 상태 |
| 멤버변수 | 클래스의 속성, 특징 |
| 메서드 | 멤버 변수를 이용하여 클래스의 기능을 구현 |
| 참조 변수 | 메모리에 생성된 인스턴스를 가리키는 변수 |
| 참조 값 | 생성된 인스턴스의 메모리 주소 값 |
