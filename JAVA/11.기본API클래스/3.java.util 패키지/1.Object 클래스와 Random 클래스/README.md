## java.util.Objects 클래스

- Object 클래스의 보조 클래스로 Object를 다루는 유용한 메서드를 제공합니다.
- util 클래스이기에 모든 메서드는 static이다.
- 주로 객체 비교 및 널  체크(Null check)에 사용된다.

```java
	static int hashCode(Object o) // 객체의 해시코드 조회 및 생성
	static int hash(Object... values) // 해시코드 생성

```

```java
	static boolean equals(Object a, Object b); // 두 객체를 비교
	static boolean deepEquals(Object a, Object b); // 두 객체를 재귀적으로 비교(다차원 배열 비교 가능 )

```

- Objects.euqals()를 사용하면 매개변수(객체)가 null인지 체크 할 필요가 없다.
- deepEquals()를 사용하면 재귀호출로 다차원 배열 비교도 가능해진다.
⇒ 그냥 equals()로 비교하려면 반복문을 통해 하나하나 갑을 추출해 비교해야 한다.
- Object.hashCode()와 동일하지만 null일때 0을 반환한다는 차이가 있다.

## java.util.Random 클래스

- 난수를 얻는 방법은 Math.random()을 사용하는 방법이 있습니다. 이 외에도 Random 클래스를 사용하면 난수를 얻을 수 있습니다.
- Math.random()은 내부적으로 Random의 인스턴스를 생성해서 사용하는 것이므로 둘 중에서 편한 것을 사용하면 된다.
- 다음 두 코드는 동일합니다.

```java
double randNum = Math.random();
double randNum = new Random().nextDouble(); // 위 문장과 동일

```

- 만약 1~6 사이의 정수를 난수로 얻고자 할 때는 다음과 같다.

```java
int num = (int)(Math.random() \* 6) + 1;
int num = new Random().nextInt(6) + 1; //

```

- Math.random()과 Random의 가장 큰 차이점은 종자값(seed)을 설정할 수 있다는 것이다. 종자값이 같은 Random인스턴스들은 항상 같은 난수를 같은 순서대로 반환하다.
- 종자값은 난수를 만드는 공식에 사용되는 값으로 같은 공식에 같은 값을 넣으면 같은 결과를 얻는 것처럼 같은 종자값을 넣으면 같은 난수를 얻게된다.

### Random 클래스의 생성자와 메서드

- 생성자 Random()은 아래와 같이 종자값을 System.currentTimeMillis()로 하기 때문에 실행할 때마다 얻는 난수가 달라진다.

> System.cyrrentTimeMillis()는 현재시간을 천분의 1초단위로 변환해서 반환한다.
> 

```
public Random() {
	this(System.currentTimeMillis());  // Random(long seed)를 호출한다.
}

```

### Random의 생성자와 메서드

| 메서드 | 설명 |
| --- | --- |
| Random() | System 현재 시간을 종자값(seed)로 이용하는 Random인스턴스를 생성한다. |
| Random(long seed) | 매개변수 seed를 종자값으로 하는 Random인스턴스를 생성한다. |
| boolean nextBoolean() | boolean 타입의 난수를 반환한다. |
| void nextBytes(byte[] bytes) | bytes배열에 byte타입의 난수를 채워서 반환한다. |
| double nextDouble() | double타입의 난수를 반환한다.(0.0 <= x < 1.0) |
| float nextFloat() | float 타입의 난수를 반환한다.(0.0 <= x <1.0) |
| int nextInt() | int타입의 난수를 반환한다(int의 범위) |
| long nextLong() | long타입의 난수를 반환한다.(long의 범위) |
| void setSeed(long seed) | 종자값을 주어진 값(seed)으로 변경한다. |

```
package day11.utils;

import java.util.Random;

public class RandomEx2 {
	public static void main(String[] args) {
		Random rand = new Random(1);
		Random rand2 = new Random(1);

		System.out.println("= rand =");
		for (int i = 0; i < 5; i++) {
			System.out.println(i + ":" + rand.nextInt());
		}

		System.out.println();
		System.out.println("= rand2 =");
		for (int i = 0; i < 5; i++) {
			System.out.println(i + ":" + rand2.nextInt());
		}
	}
}

실행결과

= rand =
0:-1155869325
1:431529176
2:1761283695
3:1749940626
4:892128508

= rand2 =
0:-1155869325
1:431529176
2:1761283695
3:1749940626
4:892128508

```
