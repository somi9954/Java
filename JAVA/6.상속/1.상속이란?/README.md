# 상속

: 부모 역할을 하는 클래스가 자식 역할을 하는 클래스에게 클래스 멤버와 메서드를 물려주는 것을 **상속**이라고 한다. (**단 생성자, 초기화 블럭은 상속되지 않습니다**)

이미 만들어진 클래스를 재사용할 수 있기 때문에 효율적이고 중복된 코드가 줄어들어 코드가 간결해져 상속을 사용한다. 즉 유지보수가 쉬워지고 확장성이 용이해지고 재사용이 가능해지고 코드가 간결해지며 시간을 단축할 수 있다.

- **클래스의 상속 방법 : extends 예약어 사용!**

클래스의 상속을 하는 방법은 다음과 같이 합니다.

```java
public B extends A {

}
```

![image](https://github.com/somi9954/Java/assets/137499604/6f19ad6c-ec9f-4ebc-a3d0-12f283724968)


부모클래스는 ‘상위클래스’ 또는 ‘슈퍼클래스’라고 불리며 자식클래스는 ‘ 하위클래스’ 또는 ‘서브클래스’ 라고 불린다.

상속을 받은 자식 클래스는 부모 클래스에 선언되어 있는 private 접근 제한을 갖는 필드와 메소드를 메서드를 제외한 public, protected, default로 선언되어 있는 모든 변수와 메서드를 물려받아 사용할 수 있습니다.

만약 부모와 자식 클래스가 서로 다른 패키지에 있다면, 부모의 default 접근 제한을 갖는 필드 및 메소드도 자식이 물려받을 수 없습니다. *(상속하는 부모 클래스는 자신이 만든 클래스가 될 수도 있고,  JDK가 지원하는 클래스가 될 수도 있습니다.)*

- **default : 아무런 접근 제한자를 명시하지 않으면 default 값이 되며, 동일한 패키지 내에서만 접근 가능합니다.**

부모 클래스가 변경되었을 때 자식 클래스는 자동으로 영향을 받게 되고, 반대로 자식 클래스의 변경은 부모에게 영향을 주지 않습니다.

자식 클래스의 멤버 개수는 부모 클래스보다 항상 같거나 많습니다.

### 상속 예시

 친구정보를 기록할 MyFriendInfo클래스를 상세정보를 기록할 MyFriendDetailInfo클래스에 상속하고 이름 나이는 MyFriendInfo클래스에
 주소와 번호는 MyFriendDetailInfo에 입력할 수 있도록 구성하시오

```java
public class MyFriendInfo {
    private String name;

    private int age;

    public MyFriendInfo(String name, int age){
        this.name = name;
        this.age = age;
    }
    public void ShowMyInfo(){
        System.out.println("이름 : " + name);
        System.out.println("나이 : " + age);
    }

}
```

```java
public class MyFriendDetailInfo extends MyFriendInfo {
     private String address;
     private String Number;

     public MyFriendDetailInfo(String name, int age, String address, String Number){
          super(name,age);
          this.address = address;
          this.Number = Number;
     }

     public void ShowMyFriendDetailInfo()
     {
          ShowMyInfo();
          System.out.println("주소: "+ address);
          System.out.println("전화: "+ Number);
     }
```

```java
public class Ex01 {
    //친구정보를 기록할 MyFriendInfo클래스를 상세정보를 기록할 MyFriendDetailInfo클래스에 상속하고 이름 나이는 MyFriendInfo클래스에
    // 주소와 번호는 MyFriendDetailInfo에 입력할 수 있도록 구성하시오
    public static void main(String[] args) {
        MyFriendDetailInfo myFriendDetailInfo = new MyFriendDetailInfo("이순신", 100, "성균관", "010-0000-0000");
        myFriendDetailInfo.ShowMyFriendDetailInfo();
    }
}
```

![image](https://github.com/somi9954/Java/assets/137499604/3dc4907f-655a-4fab-9029-f9a60b3ae278)


### static 변수의 상속

: Static 멤버는 다른 말로 클래스 멤버이다. 즉, static 멤버는 클래스당 하나만 생성되고 동일한 클래스의 객체들만 공유할 수 있다. 클래스를 상속한다는 것은 다른 클래스에서 메소드와 변수를 사용한다는 말이다. **결론적으로 static 변수는 상속의 대상이 아니다.** **하지만 접근 수준 지사자가 허용한다면 하위 클래스에서는 멤버변수의 이름만으로 접근이 가능하고, 외부에서는 객체생성 없이 클래스명을 통해서도  클래스 이름으로 접근할 수 있다. 즉 static이 가진 기본적인 규칙을 그대로 따른다.**

```java
class SuperCls {
	static int count = 0;
	
	public SuperCls() {
		count++;
	}
}

class SubCls extends SuperCls {
	
	public SubCls() {}
	public void showCount() {
		System.out.println(count); //하위 클래스에서 이름으로 접근하기
	}
}

public class FinalTermTest {
	public static void main(String[] args) {
		// TODO Auto-generated method stub
	SuperCls a1 = new SuperCls(); //1
	SuperCls a2 = new SuperCls(); //2
	SubCls b1 = new SubCls(); //3 (상속은 안되지만 참조는 가능하다)
	
	b1.showCount(); 
	System.out.println(a2.count); //외부에서 클래스 이름으로 접근하기
	}
}
```

![image](https://github.com/somi9954/Java/assets/137499604/fe93f217-9038-4382-a8b6-2d1693a42d92)


### 생성자 super()

: 부모 클래스 (하위 클래스)의 생성자를 호출할 때 쓰인다.

```java
public class Book{

}
```

```java
public class comic extends Book {
super(); //book 클래스의 기본 생성자 호출
}
```

comic 클래스에서 super() 메서드를 호출하게 되면 Book 클래스의 기본 생성자를 호출한다. 부모 객체를 생성한 후 부모 객체를 감싸고 자식 객체를 생성한다. 즉 자식 객체 안에는 부모 객체가 들어있게 된다.

생성자를 선언 시 자식 클래스에서는 반드시 부모 클래스의 생성자를 호출 해줘야 한다. 만약 부모 클래스의 생성자가 호출될 때 매개변수로 값을 전달받아 부모 클래스의 필드들을 초기화 하도록 구현되어 있다면 자식 클래스의 생성자에서 부모 클래스의 생성자를 호출할 때도 부모 클래스 대신 값을 매개변수로 받아서 부모 생성자에 넣어줘야 한다.

<aside>
💡 super() 메서드는 자식 생성자의 첫 줄에서 호출해야 한다.

</aside>

```java
public class Person{ // 클래스 선언
	String name;
	int age;

	Person(String name, int age){
	this.name = name;
	this.age = age;
 }
}
```

```java
public class Customer extends Person{ //자식 클래스 선언
	int memberId;

	Customer(String name, int age, int memberId) {
	super(name,age);     //super 메서드를 통해서 부모 생성자에 매개변수 전달
											//부모 객체 생성!
	this.memberId = memberId;   
	}
	void enter(){
	System.out.println("회원번호 : " + memberId + "(" + name + "," + age + "세)님 입장하셨습니다.");
}
```

```java
public class Ex { //클래스 선언 
public static void main(String[] args){
	Customer customer = new Customer("김이름", "20" ,"1001");
	customer.enter();
 }
}
```

![image](https://github.com/somi9954/Java/assets/137499604/a27b626d-33a2-4d6c-82cd-6148254c9590)


Customer 클래스로 객체를 만들기 위해서는 Person 객체부터 생성해야 한다. Person 생성자는 name, age를 매개변수로 받아서 객체를 생성한다. 따라서 Customer 생성자에서 Person 생성자를 호출할 때 매개변수로 받은 name, age  값을 전달하여 부모 객체를 생성하고 Customer 객체에 필요한 memberId를 추가해 Customer 객체를 완성해야 한다.
