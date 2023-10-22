## 객체 배열

객체를 저장하는 배열로 배열의 자료형을 클래스명(사용자 정의 자료형)으로 지정하여 활용할 수 있다.

객체배열은 int나 char등 기본  자료형 배열과 사용방법이 다르다.

객체 배열은 배열 안에 객체가 저장되는 것은 아니고, 객체의 주소가 저장된다.
사실 객체 배열은 참조변수들을 하나로 묶은 참조변수 배열인 것이다.

### 객체 배열의 선언과 동시에 할당

클래스명 배열명[] = new 클래스명[배열크기];

```java
Academy[] arr = new Academy[5];
```

<aside>
💡 객체를 사용하기 위해서는 Academy의 객체를 생성해 주어야 한다.

</aside>

```java
arr[1] = new Academy();
arr[2] = new Academy();
arr[3] = new Academy();
arr[4] = new Academy();
arr[5] = new Academy();
```

### 객체 배열 초기화

```java
// 1. 인덱스를 이용한 초기화
배열명[i] = new 클래스명();

arr[0] = new Academy(1, "a");
arr[1] = new Academy(2, "b");

// 2. 선언과 동시에 할당 및 초기화
클래스명 배열명[] = { new 클래스명(), new 클래스명() };

Academy arr[] = {
	new Academy(1, "a"),
	new Academy(2, "b")
};
```

### 객체배열의 호출

자료에 접근할 때는 인덱스를 활용하여 접근한다.

변수명 [인덱스]로 객체에 접근하고 멤버변수나 메소드에 접근하려면 `.` 을 이용하여 접근한다.

```java
package oop.sample;

public class Person {
	private String name; // 멤버필드
	private int age; // 멤버필드
	private char gender; // 멤버필드

	// 기본 생성자
	public Person() {
		super();
	}

	// 매개변수 있는 생성자
	public Person(String name, int age, char gender) {
		// super()를 먼저 수행하고 끝나면 아래 초기화 과정 수행함.
		super();
		this.name = name;
		this.age = age;
		this.gender = gender;
	}

	// getter, setter 메소드
	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public char getGender() {
		return gender;
	}

	public void setGender(char gender) {
		this.gender = gender;
	}

}
```

```java
package oop.test;

import oop.sample.Person;

public class TestArray {
	public static void main(String[] args) {
		// 방법 1)
		Person[] list = new Person[3]; // 3명을 보관할 수 있는 객체배열 선언
		list[0] = new Person("김개똥", 19, '남');
		list[1] = new Person("김말똥", 20, '남');
		list[2] = new Person("김소똥", 22, '여');

		// 각 객체의 멤버에 접근 이름 출력
		for(int i = 0; i < list.length; i++) {
			System.out.println(list[i].getName());
		}

		실행결과 
		김개똥
		김말똥
		김소

		// 방법 2)
		Person[] members = {
				new Person("김개똥", 19, '남'),
				new Person("김말똥", 20, '남'),
				new Person("김소똥", 22, '여')
		};

		// 각 객체의 멤버에 접근 이름 출력
		for(int i = 0; i < members.length; i++) {
			System.out.println(members[i].getName());
		}
	}
}
```

### day04/array/Book.java

```java
package day04.array;

public class Book {
	private String bookName;
	private String author;
	
	public Book() {} // 디폴트 생성자
	
	public Book(String bookName, String author) {
		this.bookName = bookName;
		this.author = author;
	}
	
	public String getBookName() {
		return bookName;
	}
	
	public void setBookName(String bookName) {
		this.bookName = bookName;
	}
	
	public String getAuthor() {
		return author;
	}
	
	public void setAuthor(String author) {
		this.author = author;
	}
	
	public void showBookInfo() {
		System.out.println(bookName + "," + author);
	}
}
```

Book 클래스는 책 이름과 저자를 멤버 변수로 가지는 클래스 입니다 .디폴드 생성자 외에도 책 이름과 저자 이름을 받는 생성자를 하나 더 구현했습니다.

### day04/array/BookArray.java

```java
package day04.array;

public class BookArray {
	public static void main(String[] args) {
		Book[] library = new Book[5];  // Book 클래스형으로 객체 배열 생성
		
		for (int i = 0; i < library.length; i++) {
			System.out.println(library[i]);
		}
	}
}

실행결과
null
null
null
null
null
```

- Book[] library = new Book[5]; 문장을 보면 Book 인스턴스 5개가 생성된 것처럼 보이나 Book 인스턴스 5개가 바로 생성되는 것은 아닙니다. 이때 만들어 지는 것은 인스턴스 주소를 담을 공간 입니다.
- Book[] library = new Book[5];는 각각의 Book인스턴스 주소 값을 담을 공간 5개를 생성하는 문장입니다.
- Book 주소값을 담을 공간이 5개 만들어 지고 자동으로 각 공간은 **비어 있다**는 의미의 null 값으로 초기화됩니다.

![image](https://github.com/somi9954/Java/assets/137499604/1b99a4b9-91d9-4a99-a034-e48eaa112c89)


### day04/array/BookArray2.java

```java
package day04.array;

public class BookArray2 {
	public static void main(String[] args) {
		Book[] library = new Book[5];
		library[0] = new Book("태백산맥", "조정래");
		library[1] = new Book("데미안", "헤르만 헤세");
		library[2] = new Book("어떻게 살 것인가", "유시민");
		library[3] = new Book("토지", "박경리");
		library[4] = new Book("어린왕자", "생텍쥐페리");
		
		for (int i = 0; i < library.length; i++) {
			library[i].showBookInfo();
		}
		
		for (int i = 0; i < library.length; i++) {
			System.out.println(library[i]);
		}
	}
}

실행결과
태백산맥,조정래
데미안,헤르만 헤세
어떻게 살 것인가,유시민
토지,박경리
어린왕자,생텍쥐페리
day04.array.Book@5e91993f
day04.array.Book@1c4af82c
day04.array.Book@379619aa
day04.array.Book@cac736f
day04.array.Book@5e265ba4
```
