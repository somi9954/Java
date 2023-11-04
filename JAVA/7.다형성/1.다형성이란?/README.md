## 다형성(polymorphism)

하나의 타입으로 다양한 객체를 사용할수 있게 되는것을 의미한다. 자바에선 대표적으로 오버로딩, 오버라이딩, 업캐스팅, 다운캐스팅, 인터페이스, 추상메소드, 추상클래스 방법이 모두 다형성에 속한다.

다형성을 활용하면 부모 클래스가 자식 클래스의 동작 방식을 알 수 없어도 오버라이딩을 통해 자식 클래스에 접근할 수 있다.

그렇다면 어떻게  부모가 자식이 어떤 일을 하는 지 몰라도,  자식 멤버 함수를 호출시킬 수 있는 이유는 **동적 바인딩** 때문입니다. **동적바인딩이란, 메서드가 실행 시점에서 성격이 결정되는 바인딩**인데요. 프로그램의 컴파일 시점에 부모 클래스는 자신의 멤버 함수밖에 접근할 수 없으나, 실행 시점에 동적 바인딩이 일어나 부모클래스가 자식 클래스의 멤버함수를 접근하여 실행할 수 있습니다.

![image](https://github.com/somi9954/Java/assets/137499604/11c149cf-614d-44a2-a66f-942224d3c051)


> 다형성은 추상 클래스, 인터페이스에서 구현됩니다. 또한 안드로이드, 스트링 등 자바 기반의 프레임워크에서 응용할 수 있는 객체 지향 프로그래밍의 중요한 개념입니다.
> 

다형성의 장점

1) 유지보수가 쉽다 : 개발자가 여러 객체를 하나의 타입으로 관리가 가능하기 때문에 코드 관리가 편리해 유지 보수가 용이하다.

2) 재사용성 증가 : 다형성을 활용하면 객체를 재사용하기 쉬워지기 때문에 개발자의 코드 재사용성이 높다.

3) 느슨한 결합 : 다형성을 활용하면 클래스간 의존성이 줄어들며 확장성이 높고 결합도가 낮아서 안정성이 높아진다.

다형성의 필수 조건

1. 상속관계 : 다형성을 활용하기 위해서는 필수로 부모클래스 - 자식 클래스 간의 클래스 상속이 이뤄져야 한다.
2. 오버라이딩 필수 (자식 클래스에서 메소드 재정의) : 다형성이 보정되기 위해서는 하위 클래스 메소드가 반드시 재정의 되어 있어야 한다.
3. 업캐스팅(자식클래스의 객체가 부모 클래스 타입
4. 으로 형변환)  : 부모 타입으로 자식클래스를 업캐스팅하여 객체를 생성해야 한다.

다형성 구현 방법

1. 상속 클래스 구현 (부모-자식 클래스 구현)
2. 메소드 오버라이딩
3. 업캐스팅하여 객체 선언
4. 부모 클래스 객체로 자식 메소드 호출

### 자료형 다형성

다형성을 활용하면 위와 같이 **부모 타입의 배열로 자식 객체들을 자유롭게 다룰 수 있습니다.**

```java
class Animal{ //공통적으로 사용하는 메서드는 상위 클래스에 선언한다.
	public void move(){
		System.out.println("동물이 움직입니다.");
    }
   }
class Human extends Animal {
   @Override
	public void move(){
	System.out.println("사람이 걷습니다.");
   }
	public void readBook(){
  System.out.println("사람이 책을 읽습니다.")
   }
 }

class Tiger extends Animal{
  @Override 
 public void move() {
	System.out.println("호랑이가 네발로 뜁니다.");
   }

	pubilc void hunting(){
	System.out.println("호랑이가 사냥을 합니다.");
  }
}

	class Eagle extends Animal{
	
  @Override
	public void move(){
		System.out.println("독수리가 하늘을 날아 다닙니다.");
    }
   public void flying(){
   System.out.println("독수리가 양날개를 쭉 펴고 날아 다닙니다.");
    }
}

```

```java
   public class AnimalTest{
     public static void main(String[] args) {
			Animal h = new Human();
      Animal t  = new Tiger();       //업캐스팅하여 객체를 선
      Animal e = new eagle();

			AnimalTest test = AnimalTest();    
      test.moveAnimal(h);
      test.moveAnimal(h);
			test.moveAnimal(e);

     System.out.println("--------------------------------");
      
		ArrayList<Animal> animalList = new ArrayList<>();
		animalList.add(h);
		animalList.add(t);
		animalList.ddd(e);
    
		for(Animal animal : animalList){
		 animal.move()
    }
   }
   public void moveAnimal(Animal animal){
		animal.move();
   }
} 
		
```

```java
출력값
사람이 걷습니다.
독수리가 하늘을 날아 다닙니다.
호랑이가 네발로 뜁니다.
-----------------------------------
사람이 걷습니다.
독수리가 하늘을 날아 다닙니다.
호랑이가 네발로 뜁니다.
```

![image](https://github.com/somi9954/Java/assets/137499604/2224c938-4fbd-4663-a2d4-fa27d2b84782)


테스트를 하기 위해 AnimalTest 클래스에 moveAnimal()메서드를 만들었다. 이 메서드는 어떤 인스턴스가 매개변수로 넘어와도 모두 Animal형으로 변환한다.

Animal에서 상속받은 클래스가 매개변수로 넘어오면 모두 Animal형으로 변환되므로 animal.move() 메서드를 호출할 수 있습니다.
가상 메서드의 원리에 따라 animal.move가 아닌 매개변수로 넘어온 실제 인스턴스의 메서드입니다.
animal.move() 코드는 변함이 없지만 어떤 매개변수가 넘어왔느냐에 따라 출력문이 달라집니다. 이것이 다형성 입니다.

### 매개변수 다형성

다형성의 특성은 **변수의 타입 뿐만 아니라 인터페이스나 파라미터에서도 똑같이 적용**됩니다.

```java
class English {
		String message = "Hello";
}

class Korean {
		String message = "안녕";
}

class French {
		String message = "Bonjour";
}

class LanguageTranslator {
		
		// 메서드 오버로딩

		void speak(English english) {
				System.out.println(english.message);
		}

		void speak(Korean korean) {
				System.out.println(korean.message);
		}

		void speak(French french) {
				System.out.println(french.message);
		}
}

public class Translator {
	public static void main(String[] args) {
			
			English english = new English();
			Korean korean = new Korean();
			French french = new French();

			LanguageTranslator papago = new LanguageTranslator();

			papago.speak(english);      // Hello 출력
			papago.speak(korean);       // 안녕 출력
			papago.speak(french);       // Bonjour 출력
	}
}
```

이렇게 메서드를 오버로딩해서 사용할 수 있습니다.

위에서 작성한 코드의 단점이 있다면, 메서드를 오버로딩 할때 각 타입별로(영어, 한국어, 프랑스어) 해주었기 때문에 만약에 독일어가 추가 된다면 메서드를 하나 더 작성해야 하는 단점이 있습니다.

타입이 추가 되더라도 수정하지 않도록 개선한 코드는 다음과 같다.

```java
interface Language {
	void speak();
}

class English implements Language {
		String message = "Hello";

		public void speak() {
			System.out.println(this.message);
		}
}

class Korean implements Language {
		String message = "안녕";

		public void speak() {
			System.out.println(this.message);
		}
}

class French implements Language {
		String message = "Bonjour";

		public void speak() {
			System.out.println(this.message);
		}
}

class LanguageTranslator {
		void translate(Language language) {
			language.speak();
		}
}

public class Translator {
	public static void main(String[] args) {
			
			English english = new English();
			Korean korean = new Korean();
			French french = new French();

			LanguageTranslator papago = new LanguageTranslator();

			papago.speak(english);      // Hello 출력
			papago.speak(korean);       // 안녕 출력
			papago.speak(french);       // Bonjour 출력
	}
}
```

이전 코드에서는 각 객체 타입마다 다른 메서드를 사용하기 위해 오버로딩을 통해 계속 메서드를 생성해야 했지만, **인터페이스를 통해 공통 메서드를 정의하고, 다른 클래스가 추가 되더라도 인터페이스를 구현 하는 것으로 구성하여 더 이상 Language 클래스의 수정 없이도 다른 결과를 출력**할 수 있도록 설계를 유연하게 변경하였습니다.

<aside>
💡 객체 지향 프로그래밍은 무언가 구현하는 프로그래밍 기법이 아니라, 개발을 용이하게 해주는 설계 기법이다.

</aside>

### 메서드 다형성

꼭 객체 타입 관점에서 뿐만 아리나 메서드를 확장하거나 재정의하는 overloading / overriding 도 메서드가 다형(多形) 해 지기 때문에 자바의 다형성 특징 중 하나에 속한다고 볼 수 있다.

```java
public class Smile { 

  smile( Parent parent ){

  parent.smile();

  }
}
public class Parent { 

  void smile ( ) { 
  System.out.println("부모님이 웃습니다");
  }
}

public class Child extends Parent { 

  @Override
  void smile( ) { 
  System.out.println("아이가 웃습니다");
  }
}
```

```java
public class SmileExample { 

Parent parent = new Parent ( ) ;
Child child = new Chile ( ) ;
Smile testSmile = new Smile ( ) ;

testSmile.smile ( parent ) ;  
testSmile.smile ( child )  ; 

}

실행결과 : 
부모님이 웃습니다.
아이가 웃습니다.
```

각각의 객체를 생성하고, 매개변수에 자식 객체를 넣게되면 자식객체에 있는 @Override smile()메소드가 실행이됩니다.
