# Record 클래스

**ㆍ** 불변(immutable) 데이터 객체를 쉽게 생성할 수 있도록 하는 새로운 유형의 클래스

**ㆍ** JDK14에서 preview로 등장하여 JDK16에서 정식 스펙으로 포함

### 기존의 불변 데이터 객체

```java
public class Person {
    private final String name;
    private final int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}
```

- 상태(name, age)를 보유하는 불변 객체를 생성하기 위한 많은 코드를 작성함
- 모든 필드에 final을 사용하여 명시적으로 정의
- 필드 값을 모두 포함한 생성자
- 모든 필드에 대한 접근자 메서드(getter)
- 상속을 방지하기 위해 클래스 자체를 final로 선언하기도함
- 로깅 출력을 제공하기 위한 toString 재정의
- 두 개의 인스턴스를 비교하기 위한 hashCode, equals 재정의
- 해당 record 클래스는 final 클래스이라 상속할 수 없다.
- 각 필드는 private final 필드로 정의된다.
- 모든 필드를 초기화하는 RequiredAllArgument 생성자가 생성된다.
- 각 필드의 getter는 getXXX()가 아닌, 필드명을 딴 getter가 생성된다.(name(), age(), address())

다음은 record 클래스의 사용법이다.

<img src="https://github.com/somi9954/Java/assets/137499604/4a8953a8-61e3-464b-9f82-a760bb266639" width="350">


```java
public record Book(int id,
                   String title,
                   String author,
                   String publisher) { } // 생성자, toString, getter, setter, hashcode 자동 생성
```

```java
package exam01;

public class Ex01 {
    public static void main(String[] args) {

    Book book = new Book(1000, " 책1", "저자1", "출판사");
        System.out.println(book);
        System.out.printf("id:%d, title:%s, author:%s, publisher:%s%n",
                book.id(), book.title(), book.author(), book.publisher());
    }
}
```

<img src="https://github.com/somi9954/Java/assets/137499604/d43990e7-40f0-4366-a865-c0b504290b44" width="500">

[내용 더 보기](https://s7won.tistory.com/2)
