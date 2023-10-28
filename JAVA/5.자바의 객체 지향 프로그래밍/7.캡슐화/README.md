### 캡슐화

캡슐화는 일반적으로 변수와 클래스를 하나로 묶는 작업이다.  캡슐화의 중요 목적은 **중요한 데이터를 보존,보호**하기 위해 사용하는 것이다.  즉 캡슐화는 클래스에 담는 내용중 중요한 데이터나 기능을 외부에서 접근하지 못하게하기 위해 사용한다고 알아 두면 된다. **캡술화 = 은닉성** 이라고 생각하면 쉽다.

캡슐화 방법

1. 멤버 변수 앞에 접근 제어자 private를 붙인다. (private: 자기 클래스에서만 접근할 수 있는 것 )
2. 멤버 변수에 값을 넣고 꺼내 올 수 있는 메소드를 만든다 (접두어 set/get을 사용해 메소드를 만든다.)

캡슐화는 다음과 같이 한다.

```java
public class Schedule2 {
    private int year;
    private int month;
    private int day;

    public int getYear() {
        return year;
    }

    public void setYear(int year) {
        this.year = year;
    }

    public int getMonth() {
        return month;
    }

    public void setMonth(int month) {
        this.month = month;
    }

    public int getDay() {
        return day;
    }

    public void setDay(int day) {
        this.day = day;
    }
}
```

```java
public class Ex01 {
    public static void main(String[] args) {
        Schedule s1 = new Schedule();

        // 멤버변수에 값을 대입 -> 통제 불가 -> 직접 값을 대입을 지양
        // 멈버변수의 접근 범위 private
        // 멤버변수를 메서드를 통해서 값을 지정 set
        // 멤버변수를 메서드를 통해서 값을 조회 get...
       
        s1.setYear(2023);
        s1.setMonth(2);
        s1.setDay(31);

        int month = s1.getMonth();
        System.out.println(month);

        s1.showDate();
    }
}
```

![image](https://github.com/somi9954/Java/assets/137499604/e4c34382-e9ee-48b8-9126-d824ecd5a840)

getter : 외부에서 변수의 데이터를 읽어올때 사용되는 메소드. Schedule2 클래스에 있는 변수(year)에 스케쥴의 year 값을 저장 

ex) public int getAge( ) { ... }

```java
 public void setYear(int year) {
        this.year = year;
    }
```

public : 어디서든 접근이 가능

void : 리턴값이 없음

setYear : 메소드이름

String year : 입력된 매개변수

this.year : Schedule2 클래스 내에 있는 private String year

setter : 외부에서 변수에 데이터를 쓰고자 할 때  사용되는 메소드. Schedule2  클래스내에 있는 변수 year에 저장되어 있는 스케쥴의 year값을 리턴

 ex) public void setAge(int age) { ... } 

```java
 public int getYear() {
        return year;
    }
```

public : 어디서든 접근이 가능

String : 리턴값의 데이터타입

getId : 메소드이름

return : 리턴

year : Schedule2 클래스 내에 있는 private String year에 저장되어 있는 값

### **사용예제**

**1) Person 클래스 정의**

1. 멤버변수 age에 **private을 사용**하여 외부에서의 직접 접근을 제한합니다.
2. 대신 age에 데이터를 쓰고 읽기위해서, **getter와 setter 메소드를 생성**해줍니다.
3. setter에서는 age에 데이터를 쓰기전, **데이터 유효성 검사 로직**을 넣어줄수 있습니다.

```java
publicclassPerson {

privateint age;

publicintgetAge() {
return age;
	}

publicvoidsetAge(int age) {
if (age >= 0) {
this.age = age;
		}
	}
}
```

**2) 객체생성 및 실행**

외부에서 Person의 인스턴스 p1의 age변수에 접근하기 위해서는 setter와 getter를 이용해서 접근할 수 있습니다.

private키워드와 함께 사용되었기 때문에 p1 변수를 외부에서 직접 접근하는 것은 불가능 합니다.

- **setter사용 : p1.setAge(20);**
- **getter사용 : p1.getAge( );**

```java
publicclassHelloWorld {
publicstaticvoidmain(String[] args) {

		Person p1 =new Person();

		p1.setAge(20);
		System.out.println(p1.getAge() + "살 입니다.");
	}
}
```

**3) 실행결과**

```java
20살 입니다.
```
