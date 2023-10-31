## final 키워드

:상수를 뜻하는 키워드로 필드 앞에 선언하여 사용한다. 초기화 이후 값을 바꿀 수 없으며 시간이 지나도 처음 정의된 상태가 변하지 않는다는 의미를 가지고 있다.

이 키워드는 변수, 메서드와 클래스에서도 사용 가능하며, 효과는 상속에서 확인할 수 있다.

| 사용 위치 | 설명 |
| --- | --- |
| 변수 | final 변수는 상수를 의미합니다. |
| 메서드 | final 메서드는 하위 클래스에서 재정의할 수 없습니다. |
| 클래스 | final 클래스는 상속할 수 없습니다. |

- **final 변수**

: final이 부여되면 변수가 상수가 된다. 상수는  변하지 않는 수를 의미하며 상수로 선언한 변수는 값을 변경할 수 없다.

이와 같이 선언한다.

```java
final 데이터형 변수명 = 값
```

- final 전역 변수인 경우

: 보통은 전역 변수로써 final과 static 키워드를 조합하여 여러 곳에서 공유하는 고정 값을 지정하여 사용한다.

```java
package day08_10.finalex;

public class Constant {
	int num = 10;
	final int NUM = 100; // 상수 선언 
	
	public static void main(String[] args) {
		Constant cons = new Constant();
		cons.num = 50;
		//cons.NUM = 200; // 상수에 값을 대입하면 오류 발생 
		
		System.out.println(cons.num);
		System.out.println(cons.NUM);
	}
}
```

- final 객체인 경우

:객체 변수의 경우 필드를 변경할 수 있지만, 객체 변수에 객체를 새로 생성하여 할당할 수 없다.

```java
class Company{
    String name = "회사명";

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}

public class Final_ex {
    public static void main(String[] args) {
    	final Company company = new Company();
    	//company = new Company(); //객체를 한번 생성했다면 재생성 불가능
    	company.setName("ex회사"); //클래스의 필드는 변경가능
    }
}
```

- final 클래스

:클래스에  final을 사용하게 되면 그 클래스는 최정상태가 되어 더이상 상속이 불가능하다. final 클래스여도 필드는 Setter함수를 통하여 변경은 가능하다. 또한 변수나 메서드를 재정의하면 기능이 정상적을 동작하지 않는 클래스에 부여해 사용한다.

final 클래스르 선언하는 방법은 다음과 같다

```java
접근제어자 final class 클래스명 {

}
```

```java
final class Fruit {
Stirng name = "Mango"
}

class Apple extends Fruti { //상속 불가

}
```

- final 메서드

:상속 받더라도 오버라이딩할 수 없는 메서드를 뜻한다.

선언하는 방법은 다음과 같다.

```java
접근제어자 final  리턴 타입 메서드 (매개변수1, 매개변수2, ...) {
   ....
}
```

```java
public class Book{
	String title;
	String author;

Book(String title, String author){
	this.title = title;
	this.author = author;
	}

final void info_title)() {
	System.out.println("책의 제목은" + title + "입니다.);
	}
void info_author(){
	System.out.println("책의 저자는" + author + "입니다.");
	}
}
```

```java
public class Comic extends Book(
	 boolean isColor;
Comic(String title, String auhtor, boolean isColor) {
	super(title, author);
	this isColor = isColor;
	}
/** @override  부모 클래스에서 final 로 선언된 메서드를 오버라이딩을 시도하면 
Cannot override the final method from parent 라는 오류가 발생된다.

final void info_title)() {
	System.out.println("책의 제목은" + title + "입니다.);
	}
*/

@Override 
void info_author(){
	System.out.println("이 만화책의 저자는" + author + "입니다.");
	}

void info_color(){
if(isColor) {
		System.out.println("이 만화책은 컬러입니다");
	} else {
		System.out.println("이 만화책은 흑백입니다");
	   }
   }
}
```

```java
package section10;

public class EX10_27 {
	public static void main(String[] args) {
		Comic comicBook = new Comic("주머니 괴물", "미상", true);
		comicBook.info_title();
		comicBook.info_author();
		comicBook.info_color();
	}
}
```

```java
출력값
책의 제목은 주머니 괴물입니다.
이 만화책의 저자는 미상입니다.
이 만화책은 컬러입니다.
```
