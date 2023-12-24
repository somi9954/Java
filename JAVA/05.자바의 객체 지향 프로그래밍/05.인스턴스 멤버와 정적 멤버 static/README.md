# 인스턴스 멤버와 정적 멤버와 static

## **인스턴스 멤버 (= 클래스 멤버)**

변수에서 그랬던 것과 같이 메서드 앞에 static이 붙어 있으면 클래스 메서드이고 붙어 있지 않으면 인스턴스 메서드이다.

모든 객체가 같은 필드 값을 가지게 할 수 있는데 일반적으로 각 객체가 가지게 되는 필드와 메서드를 인스턴스(객체) 멤버라고 말한다.

인스턴스 메서드는 인스턴스 변수와 관련된 작업을 하는, 즉 메서드의 작업을 수행하는데 인스턴스 변수를 필요로 하는 메서드이다. 그런데 인스턴스 변수는 인스턴스(객체)를 생성해야만 만들어지므로 인스턴스 메서드 역시 인스턴스를 생성해야만 호출할 수 있는 것이다.

물론 인스턴스 변수를 사용하지 않는다고 해서 반드시 클래스 메서드로 정의해야하는 것은 아니지만 특별한 이유가 없는 한 그렇게 하는 것이 일반적이다.

```java
package section07;

public class Family {
	String name; // 구성원 이름
	int age; // 구성원 나이
	String address = "서울"; // 구성원 주소
}
```

```java
package section07;

public class EX07_11 {
	public static void main(String[] args) {
		Family father = new Family();
		Family son = new Family();
		
		father.address = "인천";
		System.out.println(son.address);
	}
}

출력값
서울
```

같은 집으로 함께 이사를 한 가족이더라도 하나의 객체의 주소만 변경했더니 아들 객체의 주소는 바뀌지 않은 것을 알 수 있다. 

## 정적 멤버

- 모든 객체들이 **공유**하며 사용하는 하나의 필드와 메서드를 정적 멤버라고 한다.
- 메서드 중에서 인스턴스와 관계없는(인스턴스 변수나 인스턴스 메서드를 사용하지 않는) 메서드를 클래스 메서드(static 메서드)로 정의한다.

**static 키워드** 

static 의 사전적 의미는 ‘고정된(형용사)’라는 의미를 가지고 있다. 프로그래밍 언어에서 static은 이러한 의미를 바탕으로 ‘클래스에 고정되있다’라는 의미로 사용되고 있다. 즉 객체가 아닌 클래스에 의존적인 요소라고 생각 할 수 있다.

**static이 앞에 붙은 멤버들은 다른 멤버들과 달리 객체를 생성하지 않고 바로 사용할 수 있다.** 그 이유는 객체를 생성할 때 메모리에 올라가는 것이 아니라, 프로그램을 시작할 때 메모리에 올라가고 프로그램이 종료될 때 메모리에서 사라지기 때문이다.(데이터 영역 메모리)

정적 멤버의 경우  객체마다 가지는 데이터 기능이 아니기 때문에 모든 객체가 같은 값을 가져야 할 경우에 사용하는것이 효율적이다. 따라서 각 클래스의 멤버를 선언할 때 충분히 고려한 후 정적 멤버로 선언할지에 대한 결정을 내리는것이 좋다.

static메서드 내에 this 지역변수는 존재하지 않는다. 왜냐하면 객체 생성과 관련이 없기 때문이다.

<aside>
💡 메서드 안에 지역변수는 static을 선언할 수 없다.

</aside>

static키워드를 호출하는 방법은 다음과 같이 클래스 이름을 통해 호출한다.

```java
클래스명.필드;
클래스명.메서드();
```

  

- **static 변수**

정적인 방법으로 접근(권장)

 클래스명으로 접근

 클래스변수

예를들어 게시물의 좋아요를 누를때마다 좋아요 값을 증가시키는 LikeCount 기능을 구현한다는 가정을 해보자.

```java
package study;
public class LikeCount {
     int count;//static int count;   

public LikeCount() { 
     this.count++;        
     System.out.println("좋아요 개수 : " + count);   
      }    
public static void main(String[] args) {       
     LikeCount lc1 = new LikeCount();        
     LikeCount lc2 = new LikeCount();   
     }
}
```

위의 예제를 먼저 보면, lc1, lc2 객체가 생성될 때 lc1의 count와 lc2의 count가 서로 다른 메모리를 할당 받게된다.

```java
좋아요 개수 : 1
좋아요 개수 : 1

Process finished with exit code 0
```

그러나 아래와 같이 static변수를 사용하면 두 객체가 생성될 때 lc1, lc2 객체는 하나의 메모리를 공유하게 되는 것이다.

```java
public class LikeCount {
    //    int count;    
    static int count;   
   
    public LikeCount() {       
        this.count++;       
        System.out.println("좋아요 개수 : " + count);    
      }    
    public static void main(String[] args) {        
        LikeCount lc1 = new LikeCount();        
        LikeCount lc2 = new LikeCount();    
      }
}
```

```java
좋아요 개수 : 1
좋아요 개수 : 2

Process finished with exit code 0
```

- **static 메소드**

static메소드는 객체의 생성 없이 호출이 가능하고, 객체에서는 호출이 불가능하다.또한 static메소드 안에서는 인스턴스 변수 접근이 불가능 하다.

클래스명으로 접근 가능하다.

인스턴스 메서드 정적자원 접근가능

```java
package study;

public class LikeCount {
   int count;
   // static int count;
public LikeCount() {
   this.count++;
   System.out.println("좋아요 개수: " + count);
}
public static int getCount() {
return count; //static 메서드 안에선 인스턴스 변수는 접근이 불가하다.
}
public static void main(String[] args) {
   LikeCount lc1 = new LikeCount();
	 LikeCount lc2 = new LikeCount();
   System.out.println("총 좋아요 개수 : " + LikeCount.getCount());
  }
}
```

static메소드 안에선 static변수만 접근이 가능한 것을 볼 수 있다.

### static은 언제 사용해야 할까

1. **클래스를 설계할 때, 멤버변수 중 모든 인스턴스에 공통으로 사용하는 것에 static을 붙인다.**

: 생성된 각 인스턴스는 서로 독립적이기 때문에 각 인스턴스의 변수(iv)는 서로 다른 값을 유지한다. 그러나 모든 인스턴스에서 같은 값이 유지되어야 하는 변수는 static을 붙여서 클래스변수로 정의해야 한다.

2. **클래스 변수(static 변수)는 인스턴스를 생성하지 않아도 사용할 수 있다**.

: static이 붙은 변수(클래스변수)는 클래스가 메모리에 올라갈 때 이미 자동적으로 생성되기 때문이다.

3. **클래스 메서드(static메서드)는 인스턴스 변수를 사용할 수 없다.**

: 인스턴스 변수는 인스턴스가 반드시 존재해야만 사용할 수 있는데, 클래스메서드(static이 붙은 메서드)는 인스턴스 생성 없이 호출 가능하므로 클래스 메서드가 호출되었을 때 인스턴스가 존재하지 않을 수도 있다. 그래서 클래스 메서드에서 인스턴스변수의 사용을 금지한다.

반면에 인스턴스변수나 인스턴스메서드에서의 static이 붙은 멤버들을 사용하는 것이 언제나 가능하다. 인스턴스 변수가 존재한다는 것은 static변수가 이미 메모리에 존재한다는 것을 의미하기 때문이다.

4. **메서드 내에서 인스턴스 변수를 사용하지 않는다면, static을 붙이는 것을 고려한다.**

: 메서드의  작업내용 중에서 인스턴스변수를 필요로 한다면, static을 붙일 수 없다. 반대로 인스턴스변수를 필요로 하지 않는다면 static을 붙인다.

메서드의 호출시간이 짧아지면서 성능이 향상된다. static을 안 붙인 메서드(인스턴스메서드)는 실행 시 호출되어야할 메서드를 찾는 과정이 추가적으로 필요하기 때문에 시간이 더 걸린다.
