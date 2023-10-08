# JEP 445 : Unnamed Classes and Instance Main Methods (Preview)

## Instance Main Methods (Preview)
   
* 학생들이 대규모 프로그램을 위해 설계된 언어 기능을 이해할 필요 없이 첫 프로그램을 작성할 수 있도록 Java 언어를 진화시킵니다.

* 별도의 자바를 사용하는 것이 아니라, 학생들은 단일 수업 프로그램을 위한 간소화된 선언문을 작성하고, 그들의 실력이 성장함에 따라 더 고급 기능을 사용하도록 프로그램을 원활하게 확장할 수 있습니다.
(미리보기 언어 기능입니다.)

* 처음 자바를 배울 때 "Hello, World!"를 출력하게 되는데 프로그램이 수행하는 작업에는 너무 많은 코드, 너무 많은 개념, 너무 많은 구성 등이 너무 복잡합니다.

```JAVA
public class HelloWorld { 
    public static void main(String[] args) { 
        System.out.println("Hello, World!");
    }
}
```
* 초보자는 클래스를 선언하고 메소드를 이해하는 "public static void main"것이 다소 어려운 개념임을 알게 되는 경우가 많습니다.

* class 선언과 필수 public액세스 수정자는 대규모 프로그래밍 구조입니다. 이는 외부 구성 요소에 대한 잘 정의된 인터페이스로 코드 단위를 캡슐화할 때 유용하지만 이 작은 예제에서는 오히려 의미가 없습니다.

* String[] args변수는 코드를 외부 구성 요소(이 경우 운영 체제의 셸)와 인터페이스하기 위해 존재합니다. 한번도 사용되지 않았기에 매끄럽지 않고 도움이 되지 않습니다.

* static은 Java의 클래스 및 객체 모델의 일부입니다. 초보자에게는 static은 어렵기만 합니다. main호출하고 사용할 수 있는 더 많은 메서드나 필드를 추가하려면 학생은 해당 메서드를 모두 다음과 같이 선언해야 합니다
static. 즉, 일반적이지도 않고 좋은 습관도 아닌 관용구를 전파하거나 두 가지 사이의 차이점에 직면해야 합니다. 정적 및 인스턴스 멤버를 알아보고 개체를 인스턴스화하는 방법을 알아보세요.

* JEP의 동기는 단순히 형식을 줄이는 것이 아니라 Java 또는 일반적인 프로그래밍을 처음 접하는 프로그래머가 올바른 순서로 개념을 소개하는 방식으로 Java를 배울 수 있도록 돕는 것입니다. 
작은 개념은 실제로 유익하고 더 쉽게 이해할 수 있을 때 고급 프로그래밍 개념으로 진행됩니다.


### **실행 방법**

* 첫째, 인스턴스 기본 메서드를 허용하도록 Java 프로그램을 시작하는 프로토콜을 향상합니다 .
이러한 메소드는 매개변수가 아니며 static, 매개변수가 있을 public필요도 없습니다 String[]. 그러면 Hello, World!를 단순화할 수 있습니다.

```JAVA
class HelloWorld { 
    void main() { 
        System.out.println("Hello, World!");
    }
}
```
* 둘째, class. 선언을 암시적으로 만들기 위해 명명되지 않은 클래스를 도입합니다 
```JAVA

void main() {
    System.out.println("Hello, World!");
  }
}
```
* 이는 미리보기 언어 기능 이며 기본적으로 비활성화되어 있습니다. JDK 21에서 아래 예제를 시도하려면 다음과 같이 미리보기 기능을 활성화해야 합니다.(cmd 사용)

* java --enable-preview Main로 프로그램을 컴파일하고

```JAVA
 javac --release 21 --enable-preview Main.java
```
* 컴파일을  하게 되면 클래스 파일이 생성된다
  
![image](https://github.com/somi9954/Java/assets/137499604/82fcdb2e-2ea3-4bb5-8a4e-1591c12a23c9)

* 소스코드 런처를 사용할 때 다음과 같이 프로그램을 실행하세요.
```JAVA
java --source 21 --enable-preview Main.java
```
* 실행을 하게 되면 다음과 같이 main() 메서드 안에 있는 내용이 출력된다(PrintStream 클래스)
  
![image](https://github.com/somi9954/Java/assets/137499604/f981880f-024f-4f38-997f-eb79c1b55a7e)


* 프로그램 진입점 선언에 더 많은 유연성을 제공하고 특히 다음과 같이 인스턴스 기본 메서드를 허용하도록 시작 프로토콜을 향상합니다.

* main시작된 클래스의 메서드에 public, 또는 default 등 접근제어자 액세스 권한을 부여합니다.

* 시작된 클래스에 매개변수가 있는 static main메서드가 없지만 매개변수가 없는 메서드가 String[]포함되어 있는 경우 해당 메서드(static main)를 호출합니다.

* static main 시작된 클래스에 메서드는 없지만 private매개변수가 0이 아닌 생성자(예: of public, protected또는 패키지 액세스)와 private인스턴스 가 아닌 main메서드가 있는 경우 클래스의 인스턴스를 생성합니다. 클래스에 매개 변수가 main있는 인스턴스 메소드가 있는 경우 String[]해당 메소드를 호출하십시오. main그렇지 않으면 매개변수 없이 인스턴스 메서드를 호출합니다 .

* 이러한 변경을 통해 Hello, World!를 작성할 수 있습니다. 액세스 수정자, static수정자, String[]매개변수가 없으므로 필요할 때까지 이러한 구성의 도입을 연기할 수 있습니다.

```Java
class HelloWorld { 
    void main() { 
        System.out.println("Hello, World!");
    }
}
```
### 유연한 출시 프로토콜 
* 프로그램 진입점 선언에 더 많은 유연성을 제공하고 특히 다음과 같이 인스턴스 기본 메서드를 허용하도록 시작 프로토콜을 향상합니다.
   *  시작된 main 클래스의 메서드에 public , protected , default 등 접근 제어자의 액세스 권한을 부여한다
   *  시작된 클래스에 매개변수가 있는 static main메서드가 없지만 매개변수가 없는 메서드가 String[]포함되어 있는 경우 해당 static main 메서드를 호출합니다.
   *  static main시작된 클래스에 메서드는 없지만 private매개변수가 0이 아닌 생성자(예: of public, protected또는 패키지 액세스)와 private인스턴스 가 아닌 main메서드가 있는 경우 클래스의 인스턴스를 생성합니다. 클래스에 매개 변수가 main있는 인스턴스 메소드가 있는 경우 String[]해당 메소드를 호출하십시오. main그렇지 않으면 매개변수 없이 인스턴스 메서드를 호출합니다 .
* 이러한 변경을 통해 Hello, World!를 작성할 수 있습니다. 액세스 수정자, static수정자, String[]매개변수가 없으므로 필요할 때까지 이러한 구성의 도입을 연기할 수 있습니다.
```JAVA
class HelloWorld { 
    void main() { 
        System.out.println("Hello, World!");
    }
}
```
### 주요 메소드 선택
* 클래스를 시작할 때 시작 프로토콜은 호출할 다음 메서드 중 첫 번째 메서드를 선택합니다.
  
   * 시작된 클래스에 선언된 static void main(String[] args) static 앞에 접근제어자를 설정한다. 

   * static void main()실행된 클래스에 선언된 비공개 액세스 방법 

   * void main(String[] args)시작된 클래스에서 선언되거나 슈퍼클래스에서 상속된 비공개 액세스의 인스턴스 메서드

   * void main()시작된 클래스에서 선언되거나 슈퍼클래스에서 상속된 비공개 액세스의 인스턴스 메서드입니다 .

* public static void main(String[] args)이는 동작의 변경 사항입니다. 시작된 클래스가 인스턴스 main을 선언하면 슈퍼클래스에서 선언 된 상속된 "전통" 메서드가 아닌 해당 메서드가 호출됩니다 . 따라서 시작된 클래스가 "전통적인" 기본 메소드를 상속하지만 다른 메소드(예: 인스턴스 main)가 선택된 경우 JVM은 런타임 시 표준 오류에 대한 경고를 발행합니다.

* 선택된 메소드 main가 인스턴스 메소드이고 내부 클래스의 멤버인 경우 프로그램이 시작되지 않습니다.

## Unnamed Classes
* 이름 없는 클래스는 이름 없는 패키지에 있고, 이름 없는 패키지는 이름 없는 모듈에 있습니다. 이름 없는 패키지(여러 클래스 로더 제외)와 이름 없는 모듈은 하나만 있을 수 있지만, 이름 없는 모듈에는 이름 없는 클래스가 여러 개 있을 수 있습니다. 이름이 지정되지 않은 모든 클래스는 main메서드를 포함하므로 프로그램을 나타냅니다. 따라서 이름이 없는 패키지에 있는 이러한 여러 클래스는 여러 프로그램을 나타냅니다.

* 이름이 없는 클래스는 명시적으로 선언된 클래스와 거의 동일합니다. 해당 멤버는 동일한 수정자(예: private및 static)를 가질 수 있으며 수정자는 동일한 기본값(예: package액세스 및 인스턴스 멤버십)을 가질 수 있습니다. 한 가지 주요 차이점은 이름이 지정되지 않은 클래스에는 매개변수가 없는 기본 생성자가 있지만 다른 생성자는 있을 수 없다는 것입니다.

* 이러한 변경으로 이제 Hello, World!를 작성할 수 있습니다. 
```JAVA
void main() {
    System.out.println("Hello, World!");
}
```
* 최상위 멤버는 이름 없는 클래스의 멤버로 해석되므로 다음과 같이 프로그램을 작성할 수도 있습니다.
```JAVA
String greeting() { return "Hello, World!"; }

void main() {
    System.out.println(greeting());
}
```
* 또는 다음과 같이 필드를 사용합니다.
```JAVA
String greeting = "Hello, World!";

void main() {
    System.out.println(greeting);
}
```
* 이름 없는 클래스에 기본 main메서드가 아닌 인스턴스 메서드가 있는 경우 이를 시작하는 것은 기존 익명 클래스 선언static 구성을 사용하는 다음과 동일합니다 .
```JAVA
new Object() {
    // the unnamed class's body
}.main();
```
* 이름이 지정되지 않은 클래스를 포함하는 이름이 지정된 소스 파일은 HelloWorld.java다음과 같이 소스 코드 실행 프로그램을 사용하여 시작할 수 있습니다.
```JAVA
$ java HelloWorld.java
```
* Java 컴파일러는 해당 파일을 실행 가능한 클래스 파일로 컴파일합니다 HelloWorld.class. 이 경우 컴파일러는 HelloWorld구현 세부 사항으로 클래스 이름을 선택하지만 해당 이름은 여전히 ​​Java 소스 코드에서 직접 사용할 수 없습니다.
* javadoc이름 없는 클래스는 다른 클래스에서 액세스할 수 있는 API를 정의하지 않으므로 이름 없는 클래스가 있는 Java 파일에 대한 API 문서를 생성하라는 요청을 받으면 도구가 실패합니다 . 이 동작은 향후 릴리스에서 변경될 수 있습니다.
* 이 Class.isSynthetic메서드는 true이름이 지정되지 않은 클래스에 대해 반환됩니다.
