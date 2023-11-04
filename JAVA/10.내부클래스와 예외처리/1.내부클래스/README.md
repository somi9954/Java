# 내부 클래스

: **클래스 안에 정의된 클래스** 중첩 클래스라고 한다.

내부 클래스를 사용하는 이유는 다음과 같다.

- 두 클래스를 멤버들 간에 손쉽게 접근할 수 있다.
- 불필요한 클래스를 감춰서 코드의 복잡성을 줄일  수 있다(캡슐화)
- 내부 클래스도 클래스이기 때문에 외부 클래스의 멤버와 같이 간주되고, 인스턴스 멤버와 static 멤버 간의 규칙이 내부 클래스에도 똑같이 적용된다.  그리고 abstract나 final 같은 제어자를 사용할 수 있을뿐만 아니라, 멤버변수들처럼 private, protected과 접근제어자도 사용이 가능하다.
- final 과 static이 동시에 붙은 변수는 상수(constant)이므로 모든 내부 클래스에서 정의가 가능하다.

내부클래스를 예를 들면 다음과 같다.

```java
public class OuterClass{ //외부클래스
  ... 
    class InnerCalss { //내부 클래스 
       ...
   }
}
```

내부클래스의 종류에는 클래스 안에서 선언된 위치에 따라 구분되어진다.

|        내부 클래스 |                                                                 특           징 |
| --- | --- |
| 인스턴스 클래스 (instance class) |외부 클래스의 멤버변수 선언위치에 선언하며, 외부 클래스의 인스턴스 멤버처럼 다루어진다. 주로 외부 클래스의 인스턴스멤버들과 관련된 작업에 사용될 목적으로 선언된다. |
|  정적 클래스 (static class) | 외부 클래스의 멤버변수 선언위치에 선언하며, 외부 클래스의 static 멤버처럼 다루어진다. 주로 외부 클래스의 static 멤버, 특히 static 메서드에서 사용될 목적으로 사용된다. |
|  지역 클래스 (local class) |  외부 클래스의 메서드나 초기화블럭 안에 선언하며,  선언된 영역 내부에서만 사용될 수 있다. |
|  익명 클래스 (anonymous class) |    클래스의 선언과 객체의 생성을 동시에 하는 이름 없는 클래스 ( 일회용) |


```java
class ABC { // 외부 클래스
	class In { // 인스턴스 내부 클래스
	
	}
	
	static class Sin { // 정적 내부 클래스
	
	}
	
	public void abc() {
		class Local { // 지역 내부 클래스
		
		}
	}
}
```

### 인스턴스 내부 클래스

- 인스턴스 변수, 인스턴스 메서드와 비슷하게 동작
- 객체가 생성되어야 접근 가능한 변수, 메서드
- 정적 변수, 정적 메서드 -> 객체 생성과 상관 없이 사용 가능
- 객체 생성된 이후 존재하는 인스턴스 내부 클래스는 정적 메서드를 정의 x ->JDk15
- 외부 클래스의 객체가 생성되어야 생성할 수 있는(정적 자원) 클래스 JDK 16부터 정의 가능

**인스턴스 클래스의 생성은 다음과 같다.**

인스턴스 멤버와 동일한 위치에 생성된다.

```java
 public class Outer {
		private String name; //인스턴스 멤버
 
  ...

		public class Inner { //인스턴스 클래스
			 private String name;
			 ...

   }
}
```

다음은 인스턴스 클래스를 선언하는 방법은 다음과 같다.

```java
Outer outer = new Outer(); // 외부 클래스 객체 생성
Outer.Inner in = outer.new Inner(); // 외부 클래스를 이용해 내부 클래스 객체 생
```

```java
package section13;

class Calculator {
	private int val1; // 인스턴스 멤버
	private int val2;

	// 생성자를 통한 데이터 입력
	public Calculator(int val1, int val2) {
		this.val1 = val1;
		this.val2 = val2;
	}
	public class Calc { // 인스턴스 클래스를 구현한다.
		public int add() {
			return val1 + val2;  //외부 클래스 멤버를 이용하여 계산한다.
		}
	}
}
public class CalculatorExample {
	public static void main(String[] args) {
		Calculator cal = new Calculator(10, 11); // 외부 클래스 선언 매개변수로 10과 11을 넣는다.
		Calculator.Calc c = cal.new Calc(); // 인스턴스 클래스 선언
		System.out.println("합 : " + c.add());
	}
}

출력값 
합 : 20
```

### 정적 내부 클래스(static)

- 정적 변수, 정적 메서드와 비슷하게 동작
- 외부 클래스가 객체가 되는 조건과 상관없다.
- 외부 클래스의 생성과 상관 없이 정적인 방법으로 독자 생성 가능!!
- 일반 클래스 정의와 큰 차이는 X
- 유일하게 static멤버를 가질 수 있다.

정적 내부 클래스의 생성은 인스턴스 멤버와 동일한 위치에 선언한다.

```java
 public class Outer {
		private String name; //인스턴스 멤버
 
  ...

		public static class Inner { //정적 내부 클래스
			 private String name;
			 ...

   }
}
```

외부 클래스의 변수 또는 메서드는 정적 내부 클래스 안에서는 사용할 수 없다.

```java
public class OuterClass { //외부 클래스
	private int vla;  // 인스턴스 변수
	private static int cnt = 1; // 클래스변수(static)
  
	public static class NestedClass{
		public void displayOuterInfo() {
			//오류발생
			//인스턴스 멤버는 정적 내부 클래스 내의 메서드에서 사용 불가
			//System.out.println(vla);
			//정적 변수는 사용가능
			System.out.println(cnt);
	 		}
 	 }
}
```

정적 내부 클래스는 인스턴스 클래스와 다르게 외부 클래스 객체를 생성하지 않아도 선언할 수 있다.정적 내부 클래스 선언하는 방법은 다음과 같다.

```java
Outer.Inner in = new Oute.Inner(); //외부 클래스 없이 바로 객체 생성 
```

```java
package exam02;

public class OutClass {
    private int num = 10; // 외부 클래스 private 변수
    private static int sNum = 20; // 외부 클래스 정적 변수

    static class InStaticClass { // 정적 내부 클래스
        int inNum = 100; // 정적 내부 클래스의 인스턴스 변수
        static int sInNum = 200; // 정적 내부 클래스의 정적 변수

        // 정적 내부 클래스의 일반 메서드
        void inTest() {
            //num += 10; // 외부 클래스의 인스턴스 변수는 사용할 수 없다.
            System.out.println("InStaticClass inNum = " + inNum + "(내부 클래스의 인스턴스 변수 사용)");
            System.out.println("InStaticClass sInNum = " + sInNum + "(내부 클래스의 정적 변수 사용)");
            System.out.println("OutClass sNum = " + inNum + "(외부 클래스의 정적 변수 사용)");
        }

        // 정적 내부 클래스의 정적 메서드
        static void sTest() {
            // 외부 클래스와 내부 클래스의 인스턴스 변수는 사용할 수 없다.
            //num += 10;
            //inNum += 10
            System.out.println("OutClass sNum = " + sNum + "(외부 클래스의 정적 변수 사용)");
            System.out.println("InStaticClass sInNum = " + sInNum + "(내부 클래스의 정적 변수 사용)");

        }
    }

}
```

```java
package exam02;

public class InnerTest {
    public static void main(String[] args) {

        OutClass.InStaticClass sInClass = new OutClass.InStaticClass();
        System.out.println("정적 내부 클래스 일반 메서드 호출");
        sInClass.inTest(); //100(내부클래스 인스턴스변수), 200(내부클래스 정적변수), 20(외부클래스 정적변수)
        System.out.println();
        System.out.println("정적 내부 클래스의 정적 메서드 호출");
        OutClass.InStaticClass.sTest(); //20(외부클래스 정적변수) , 200(내부클래스 정적변수)
    }
}
```

![image](https://github.com/somi9954/Java/assets/137499604/b6555268-18f1-4a99-8e9f-a77411398ab7)


<aside>
💡 참고)
정적 메서드
-인스턴스 자원 접근 불가(this가 존재 X)

</aside>

| 정적 내부 클래스 메서드 | 변수 유형 | 사용 가능 여부 |
| --- | --- | --- |
| 일반 메서드void inTest() | 외부 클래스의 인스턴스 변수(num) | X |
|  | 외부 클래스의 정적변수(sNum) | O |
|  | 정적 내부 클래스의 인스턴스 변수(inNum) | O |
|  | 정적 내부 클래스의 정적 변수(sInNum) | O |
| 정적 메서드static void sTest() | 외부 클래스의 인스턴스 변수(num) | X |
|  | 외부 클래스의 정적변수(sNum) | O |
|  | 정적 내부 클래스의 인스턴스 변수(inNum) | X |
|  | 정적 내부 클래스의 정적 변수(sInNum) | O |

### 지역 내부 클래스

- 메서드(함수)안(내부)에 정의된 클래스
- 인터페이스,추상클래스 → 객체가 될 수 있다.
- 외부 클래스의 메서드 내에서 선언되어 사용하는 클래스. 메서드 내에서 선언되기 때문에 해당 클래스는 메서드 내에서만 사용할 수 있다. 메서드의 실행이 끝나면 해당 클래스도 사용이 종료된다.

**지역클래스의 생성은 다음과 같다.**

지역 클래스는 다음과 같이 메서드 내에서 선언하고 사용한다.

```java
 public class Loclaclass {
	...
		public void point() { 
      ...
        class A {     //지역 클래스 선언
          ...
				}

			A a = new A();   //메서드 내에서 사용

   }
}
```

```java
pacakage innerclass;

class Outer{
    int outNum = 100;
    static int sNum = 200;
    
    Runnable getRunnable(int i){
        int num = 100;				//지역변수 : 메서드가 호출될때 스택메모리에 생성되고 메서드 수행끝날때 메모리에서 사라짐.
        
        class MyRunnable implements Runnable {	//지역 내부 클래스
            int localNum = 10;			//지역 내부 클래스의 인스턴스 변수
            
            @Override
            public void run(){
                //num = 200;			//지역변수는 상수로 바뀌므로 값을 변경할수없어 오류 발생
                //i = 100;			//매개변수도 지역변수처럼 상수로 바뀌므로 값을 변경할수 없어 오류발생
                System.out.println("i = " + i);	//10
                System.out.println("num = " + num);	//100
                System.out.println("localNum = " + localNum);	//10
                System.out.println("outNum = " + outNum + "(외부클래스 인스턴스변수)");	//100
                System.out.println("Outer.sNum = " + Outer.sNum + "(외부클래스 정적변수)");	//200
            }
        }
        return new MyRunnable();
    }
}

public class LocalInnerTest {
    public static void main(String[] args){
        Outer out = new Outer();
        Runnable runner = out.getRunnable(10);	//메서드 호출
        runner.run();
    }
```

![image](https://github.com/somi9954/Java/assets/137499604/61aa11e9-c27b-4dc1-ad1c-977ea16e482c)


<aside>
💡 추상클래스, 인터페이스가 객체가 될 수 있는 조건?
1)지역 안에서 생성, 멤버 변수에서 생성
2)멤버 변수
3)미구현된 메서드를 구현 함으로써 생성 가능
→지역 내부에 정의된 클래스의 메서드에서 지역 변수를 사용→ 스택에서 제거 X → 지역변수를 상수화 (final) - 데이터 영역

</aside>

```java
public class InnerExam3 {
    public void exec(){ 	//메소드
        class Cal{ 			//지역 내부 클래스
            int value = 0;
            public void plus(){
                value++;
            }
        }
        /* 메소드 안에서만 Cal 객체 생성 및 메소드 호출 */
        Cal cal = new Cal();
        cal.plus();
        System.out.println(cal.value);
    }
}

```

지역 내부 선언된 클래스는 메소드 안에서만 객체 생성 및 메소드 호출이 가능하다.

```java
    public static void main(String[] args) {
        InnerExam3 t = new InnerExam3();
        t.exec();
    }
```

### 익명 내부 클래스

- 클래스 이름을 사용하지 않는 클래스가 있다. 이런 클래스를 익명 클래스라고 부른다.
- 조상클래스의 이름이나 구현하고자 하는 인터페이스의 이름을 사용해서 정의하기 때문에 하나의 클래스로 상속받는 동시에 인터페이스를 구현하거나 둘 이상의 인터페이스를 구현할 수 없다. 오로지 단 하나의 클래스를 상속받거나 단 하나의 인터페이스만 구현할 수 있다.
- 하위 클래스르 한 번만 사용하고 말 것 이라면 굳이 상속하지 않고 사용할 수 있는 것이 익명 클래스이다.

익명 내부 클래스의 사용방법은 다음과 같다.

```java
Person p = new Person();

Person p = new Person(){
	 @override
	void method(){
  }
  ...
};
```

```java
new 부모 추상클래스명(){
    // 부모 추상클래스 추상 메소드 오버라이딩
};

new 부모 인터페이스명(){
    // 부모 인터페이스 메소드 오버라이딩
};
```

### **OuterInter.java**

> OuterInter 인터페이스가 선언된 파일
> 

```java
package j200204;

public interface OuterInter {

    public void interPrint();

}
```

### **OuterInner.java**

> 추상 클래스 Abs를 선언하고
> 

```java
package j200204;

// 추상 클래스 선언abstract class Abs {

// 추상 메소드abstract public void absPrint();

// 일반 메소드public void print() {
        System.out.println("추상 클래스 일반 메소드 호출");
    }
}

// 외부 클래스public class OuterInner {

// 추상 클래스 상속 내부 익명 클래스 객체 생성// 추상 클래스를 상속했기 때문에 자료형은 추상 클래스를 따름
    Abs abs = new Abs() {
        public void absPrint() {
            System.out.println("추상 클래스 상속 내부 익명 클래스");
        }
    };

// 인터페이스 구현 내부 익명 클래스 객체 생성// 인터페이스를 구현했기 때문에 자료형은 인터페이스를 따름
    OuterInter oi = new OuterInter() {
        public void interPrint() {
            System.out.println("인터페이스 구현 내부 익명 클래스 ");
        }
    };

    public static void main(String[] args) {

// 외부 클래스 객체 생성
        OuterInner outin = new OuterInner();

// 외부 클래스 객체에서 인터페이스 객체의 재정의된 interPrint() 메소드 호출
        outin.oi.interPrint();

// 추상 클래스 객체의 재정의된 absPrint() 메소드 호출
        outin.abs.absPrint();

// 추상 클래스 객체의 일반 메소드 역시 호출 가능
        outin.abs.print();

/*
        인터페이스 구현 내부 익명 클래스
        추상 클래스 상속 내부 익명 클래스
        추상 클래스 일반 메소드 호출
        */
    }

}
```

## 내부클래스의 접근 제한

내부 클래스도 클래스이기 때문에 접근 제한자를 붙여서 사용할 수 있다. 

```java
package section13;

public class PermitExample {
	private class InClass {  //인스턴스 클래스를 private로 선언
		public void print() {
			System.out.println("접근을 private로 제한합니다.");
		}
	}
	
	public InClass getInClass() {   //private로 선언된 객체를 받기 위해 메서드 생성
		// 인스턴스 클래스를 선언하여 리턴
		return new InClass();
	}
	public static void main(String[] args) {
		PermitExample permit = new PermitExample();
		permit.getInClass().print();  //메서드를 통해서 인스턴스 클래스를 받음
	}
}

출력값 
접근을 private로 제한합니다.
```

인스턴스 클래스를 private로 선언하여 getter를 통해서 클래스를 얻도록 제한했다. 이처럼 내부 클래스도 접근 제한자를 통해 제한할 수 있다.

지역클래스는 메서드 내에서 선언되어 사용한다. 보통 메서드가 종료되면 클래스도 함께 종료되지만 메서드와 실행되는 위치기 다르기 때문에 종료되지 않고 남을수도 있다. 그래서 지역 클레스에서 메서드 내의 변수를 사용할 때는 변수를 복사해서 사용한다. 이러한 이유로 지역 클래스에서 메서드의 변수를 사용할 때 해당 변수가 변경되면 오류가 발생 된다.

```java
package section13;

public class LocalClassExample {
	private int speed = 10;
	
	public void getUnit(String unitName) {
		
		class Unit {
			public void move() {
				System.out.println(unitName + "이 " + speed + " 속도로 이동합니다.");
			}
		}
		Unit unit = new Unit();
		unit.move();
	}
	
	public static void main(String[] args) {
		LocalClassExample local = new LocalClassExample();
		local.getUnit("마린");
	}
}
```

매개변수로 넘어온 untiName변수에 ‘님’이라는 글자를 추가하면  move 메서드 안에 있는 print() 메서드에서 오류가 발생된다. 자바7버전까지는 지역 클래스에서 메서드의 변수를 사용하려면 final 키워드를 붙여서 사용하도록 하였으나 자바8부터는 해당 변수를 변경하지 않는다는 조건하에 effective final이라는 기능이 추가되어 키워드를 사용하지 않아도 final변수로 인정된다.

| 종류 | 구현위치 | 사용할 수 있는 외부 클래스 변수 | 생성방법 |
| --- | --- | --- | --- |
| 인스턴스 내부 클래스 | 외부 클래스 멤버 변수와 동일 | 외부 인스턴스 변수외부 전역 변수 | 외부 클래스를 먼저 만든 후 내부 클래스 생성 |
| 정적 내부 클래스 | 외부 클래스 멤버 변수와 동일 | 외부 전역 변수 | 외부 클래스와 무관하게 생성 |
| 지역 내부 클래스 | 메서드 내부에 구현 | 외부 인스턴스 변수외부 전역 변수 | 메서드를 호출할 때 생성 |
| 익명 내부 클래스 | 메서드 내부에 구현변수에 대입하여 직접 구현 | 외부 인스턴스 변수외부 전역 변수 | 메서드를 호출할 떄 생성되거나, 인터페이스 타입 변수에 대입할 때 new 예약어를 사용하여 생성 |
