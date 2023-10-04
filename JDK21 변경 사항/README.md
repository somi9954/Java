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
*초보자는 클래스를 선언하고 메소드를 이해하는 "public static void main"것이 다소 어려운 개념임을 알게 되는 경우가 많습니다.

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



