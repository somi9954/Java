# 열거형(enums)

## 열거형이란?

- 상수만을 위한 클래스
- 자바는 C언어와 달리 열거형라는 것이 존재하지 않았으나 JDK5부터 추가되었다.
- 자바의 열거형은 C언어의 열거형보다 더 향상된 특징을 가진다.
- 값뿐만 아니라 타입까지 체크하여 타입에 안전하다
- 정적 함수 객체가 되어서 사용할 수 있다.
- 상수의 값이 바뀌면 해당 상수를 참조하는 모든 소스를 다시 컴파일 해야 한다. 그러나 열거형 상수를 사용하면, 기존의 소스를 다시 컴파일하지 않아도 된다.

```java
class Card {
	enum Kind { CLOVER, HEART, DIAMOND, SPADE } // 열거형 Kind를 정의
	enum Value { TWO, THREE, FOUR }  // 열거형 Value를 정의

	final Kind kind;
	final Value value;
}

```

## 열거형 정의와 사용

```java
enum 열거형이름 { 상수명1, 상수명2, ... }

```

- 사용하는 방법은 **열거형 이름.상수명**이다
- 클래스의 static 변수를 참조하는 것과 동일

```java
enum Direction { EAST, SOUTH, WEST, NORTH }

class Unit {
	int x, y; // 유닛의 위치
	Direction dir; // 열거형을 인스턴스 변수로 선언

	void init() {
		dir = Direction.EAST; // 유닛의 방향을 EAST로 초기화
	}
}

```

- 열거형 상수간의 비교에는 '=='를 사용할 수 있다.(상수의 주소를 비교하므로)
- '<', '>'와 같은 비교연산자는 사용할 수 없고 compareTo()는 사용가능하다.

```java
	if (dir == DIRECTION.EAST) {
		x++;
	} else if (dir > Direction.WEST) { // 에러. 열거형 상수에 비교연산자 사용불가.
		...
	} else if (dir.compareTo(Direction.WEST) > 0) { // compareTo()는 가능
		...
	}

```

- switch문 조건식에도 열거형을 사용할 수 있다.
- 주의할 점은 case문에 열거형의 이름은 적지 않고 상수의 이름만 적어야 한다.

```java
	void move() {
		switch(dir) {
			case EAST: x++; // Direction.EAST라고 쓰면 안된다.
				break;
			case WEST: x--;
				break;
			case SOUTH: y++;
				break;
			case NORTH: y--;
				break;
		}
	}

```

### 모든 열거형의 상위 클래스 - java.lang.Enum

```java
Direction[] dArr = Direction.values();

for(Direction d : dArr) {
	System.out.printf("%s = %d%n", d.name(), d.ordinal());
}

```

- values()는 열거형의 모든 상수를 배열에 담아서 반환한다.
- 이 메서드는 모든 열거형이 가지고 있는 것으로 컴파일러가 자동으로 추가해 준다.
- ordinal()은 모든 열거형의 상위 클래스인 java.lang.Enum 클래스에 정의된 것으로 열거형 상수가 정의된 순서(0부터 시작)를 정수로 반환한다

### Enum 클래스에 정의된 메서드

| 메서드 | 설명 |
| --- | --- |
| Class<E> getDeclaringClass() | 열거형의 Class 객체를 반환한다. |
| String name() | 열거형 상수의 이름을 문자열로 반환한다. |
| int ordinal() | 열거형 상수가 정의된 순서를 반환한다.(0부터 시작) |
| T valueOf(Class<T> enumType, String name) | 지정된 열거형에서 name값과 일치하는 열거형 상수를 반환한다. |

### 컴파일러가 자동으로 추가해주는 메서드

```java
static E values() static E valueOf(String name)
```

- 열거형 상수의 이름으로 문자열 상수에 대한 참조를 얻을 수 있게 해준다.

```java
Direction d = Direction.valueOf("WEST");

System.out.println(d); // WEST
System.out.println(Direction.WEST == Direction.valueOf("WEST")); // true

```

day16/EnumEx1.java
```java
package day16;

enum Direction { EAST, SOUTH, WEST, NORTH };

public class EnumEx1 {
	public static void main(String[] args) {
		Direction d1 = Direction.EAST;
		Direction d2 = Direction.valueOf("WEST");
		Direction d3 = Enum.valueOf(Direction.class, "EAST");

		System.out.println("d1=" + d1);
		System.out.println("d2=" + d2);
		System.out.println("d3=" + d3);

		System.out.println("d1==d2 ? " + (d1 == d2)); // false
		System.out.println("d1==d3 ? " + (d1 == d3)); // true
		System.out.println("d1.equals(d3) ? " + d1.equals(d3)); // true
		// System.out.println("d2 > d3 ? " + (d1 > d3)); // 에러
		System.out.println("d1.compareTo(d3) ? " + (d1.compareTo(d3))); // 0
		System.out.println("d1.compareTo(d2) ? " + (d1.compareTo(d2)));

		switch(d1) {
			case EAST: // Direction.EAST라고 쓸 수 없다.
				System.out.println("The direction is EAST."); break;
			case SOUTH:
				System.out.println("The direction is SOUTH."); break;
			case WEST:
				System.out.println("The direction is WEST."); break;
			case NORTH:
				System.out.println("The direction is NORTH"); break;
			default:
				System.out.println("Invalid direction.");
		}

		Direction[] dArr = Direction.values();

		for(Direction d : dArr) {
			System.out.printf("%s=%d%n", d.name(), d.ordinal());
		}
	}
}

실행 결과

d1=EAST
d2=WEST
d3=EAST
d1==d2 ? false
d1==d3 ? true
d1.equals(d3) ? true
d1.compareTo(d3) ? 0
d1.compareTo(d2) ? -2
The direction is EAST.
EAST=0
SOUTH=1
WEST=2
NORTH=3

```

## 열거형에 멤버 추가하기

- Enum클래스에 정의된 ordinal()이 열거형 상수가 정의된 순서를 반환하지만, 이 값을 열거형 상수의 값으로 사용하지 않는 것이 좋다. 이 값은 내부적인 용도로만 사용되기 위한 것이다.
- 열거형 상수의 값이 불연속적인 경우에는 다음과 같이 열거형 상수의 이름 옆에 원하는 값을 괄호()와 함게 적어주면 된다.

```java
enum Direction { EAST(1), SOUTH(5), WEST(-1), NORTH(10) }

```

- 지정된 값을 값을 저장할 수 있는 인스턴스 변수와 생성자를 새로 추가해 주어야 한다.
- 생성자는 private로만 생성이 된다.
- 주의할 점
    - 열거형 상수를 모두 정의한 다음에 다른 멤버들을 추가해야 한다.
    - 열거형 상수의 마지막에 ';'를 추가해야 한다.

```java
enum Direction {
	EAST(1), SOUTH(5), WEST(-1), NORTH(10); // 끝에 ';'를 추가해야 한다.

	private final int value; // 정수를 저장할 필드(인스턴스 변수)를 추가
	Direction(int value) { this.value = value; } // 생성자를 추가

	public int getValue() { return value; } // 외부에서 이 값을 얻을 수 있도록 추가
}

```

- 열거형 생성자는 외부에서 호출이 불가하다. 열거형의 생성자는 제어자가 묵시적으로 private이다

```java
Direction d = new Direction(1); // 에러, 열거형의 생성자는 외부에서 호출 불가

```

```java
enum Direction {
	...
	Direction(int value) {  // private Direction(int value)와 동일
		this.value = value;
	}
	...
}

```

- 열거형 상수에 여러값을 지정할 수 있다. 다만 그에 맞게 인스턴스 변수와 생성자 등을 추가해야 한다.

```java
enum Direction {
	EAST(1, ">"), SOUTH(2, "V"), WEST(3, "<"), NORTH(4, "^");

	private final int value;
	private final String symbol;

	Direction(int value, String symbol) { // 접근 제어자 private이 생략됨
		this.value = value;
		this.symbol = symbol;
	}

	public int getValue() { return value; }
	public String getSymbol() { return symbol; }
}

```

day16/EnumEx2.java
```java
package day16;

enum Direction2 {
	EAST(1, ">"), SOUTH(2, "V"), WEST(3, "<"), NORTH(3, "^");

	private static final Direction2[] DIR_ARR = Direction2.values();
	private final int value;
	private final String symbol;

	Direction2(int value, String symbol) { // 접근 제어자 private이 생략됨
		this.value = value;
		this.symbol = symbol;
	}

	public int getValue() { return value; }
	public String getSymbol() { return symbol; }

	public static Direction2 of(int dir) {
		if (dir < 1 || dir > 4) {
			throw new IllegalArgumentException("Invalid value : " + dir);
		}

		return DIR_ARR[dir - 1];
	}

	// 방향을 회전시키는 메서드. num의 값만큼 90도씩 시계방향으로 회전한다.
	public Direction2 rotate(int num) {
		num = num % 4;

		if (num < 0) num += 4; // num이 음수일 때는 시계반대 방향으로 회전

		return DIR_ARR[(value - 1 + num) % 4];
	}

	public String toString() {
		return name() + getSymbol();
	}
}

public class EnumEx2 {
	public static void main(String[] args) {
		for(Direction2 d : Direction2.values()) {
			System.out.printf("%s=%d%n", d.name(), d.getValue());
		}

		Direction2 d1 = Direction2.EAST;
		Direction2 d2 = Direction2.of(1);

		System.out.printf("d1=%s, %d%n", d1.name(), d1.getValue());
		System.out.printf("d2=%s, %d%n", d2.name(), d2.getValue());

		System.out.println(Direction2.EAST.rotate(1));
		System.out.println(Direction2.EAST.rotate(2));
		System.out.println(Direction2.EAST.rotate(-1));
		System.out.println(Direction2.EAST.rotate(-2));

	}
}

실행결과
EAST=1
SOUTH=2
WEST=3
NORTH=3
d1=EAST, 1
d2=EAST, 1
SOUTHV
WEST<
NORTH^
WEST<

```

### 열거형에 추상메서드 추가하기

- 열거형에 추상 메서드를 선언하면 각 열거형 상수가 이 추상 메서드를 반드시 구현해야 한다.
- 추상클래스나 인터페이스를 가지고 추상 메서드를 구현함으로써 익명 클래스를 작성하는 것과 유사하다

```java
enum Transportation {
	BUS(100) { int fare(int distance) { return distance * BASIC_FARE; }},
	TRAIN(150) { int fare(int distance) { return distance * BASIC_FARE; }},
	SHIP(100)  { int fare(int distance) { return distance * BASIC_FARE; }},
	AIRPLANE(300)  { int fare(int distance) { return distance * BASIC_FARE; }};

	abstract int fare(int distance); // 거리에 따른 요금을 계산하는 추상 메서드

	protected final int BASIC_FARE; // protected로 해야 각 상수에서 접근가능

	Transportation(int basicFare) {
		BASIC_FARE = basicFare;
	}

	public int getBasicFare() { return BASIC_FARE; }
}

```

day16/EnumEx3.java
```java
package day16;

enum Transportation {
	BUS(100) { int fare(int distance) { return distance * BASIC_FARE; }},
	TRAIN(150) { int fare(int distance) { return distance * BASIC_FARE; }},
	SHIP(100)  { int fare(int distance) { return distance * BASIC_FARE; }},
	AIRPLANE(300)  { int fare(int distance) { return distance * BASIC_FARE; }};

	abstract int fare(int distance); // 거리에 따른 요금을 계산하는 추상 메서드

	protected final int BASIC_FARE; // protected로 해야 각 상수에서 접근가능

	Transportation(int basicFare) {
		BASIC_FARE = basicFare;
	}

	public int getBasicFare() { return BASIC_FARE; }
}

public class EnumEx3 {
	public static void main(String[] args) {
		System.out.println("bus fare=" + Transportation.BUS.fare(100));
		System.out.println("train fare=" + Transportation.TRAIN.fare(100));
		System.out.println("ship fare=" + Transportation.SHIP.fare(100));
		System.out.println("airplane fare=" + Transportation.AIRPLANE.fare(100));
	}
}

실행결과
bus fare=10000
train fare=15000
ship fare=10000
airplane fare=30000

```
