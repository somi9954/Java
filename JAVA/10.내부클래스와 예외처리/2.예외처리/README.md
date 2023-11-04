# 예외처리

## 예외 클래스

### **오류와 예외**

오류(Error) 

- 시스템적인 오류(인프라 ... )
- 개발자가 통제 X
- 오류에 대한 처리는 불가하다.

예외(Exception) 

- 프로그램 소스상의 오류
- 개발자가 통제 O

![image](https://github.com/somi9954/Java/assets/137499604/c6adbd78-6511-40de-9ff1-c4f4492355d0)


• 오류 클래스는 모두 **Throwable 클래스**에서 상속받습니다. **Error 클래스**의 하위 클래스는 시스템에서 발생하는 오류를 다루며 프로그램에서 제어하지 않습니다. 프로그램에서 제어하는 부분은 **Exception 클래스**와 그 하위에 있는 예외 클래스 입니다.

---

### 오류**란 ?**

- **컴파일 오류(compile error)**
    - 프로그램 코드 작성 중 실수로 발생하는 오류
    - 발생한 컴파일 오류를 모두 수정해야 프로그램이 정상적으로 실행 되므로, 문법적으로 오류가 있다는 것을 바로 알 수 있습니다.
- **실행(런타임) 오류(runtime error)**
    - 실행 중인 프로그램이 의도하지 않은 동작을 하거나 프로그램이 중지되는 오류 입니다. 실행 오류 중 프로그램을 잘목 수현하여 의도한 바와 다르게 실행되어 생기는 오류를 **버그(bug)**라고 합니다.
    - 프로그램 실행 중에 발생하는 오류는 예측하기 어려운 경우가 많고, 프로그램이 비정상 종료되면서 갑자기 멈춰 버립니다.
    - 자바은 이러한 비정상 종료를 최대한 줄이기 위해 다양한 예외에 대한 처리방법을 가지고 있습니다.
    - 예외 처리를 하는 목적은 프로그램이 비정상 종료 되는 것을 방지하기 위한 것 입니다.
    
    ---
    

### 예외클래스의 종류

![image](https://github.com/somi9954/Java/assets/137499604/ff05303e-7685-47ac-a405-30df0345e6ee)


- **Throwable**
    - Exception을 바로 상속 받는 예외
    - 예)IOException
    ↳ FileNotFoundException
    
    - 예외의 확인이 컴파일 시점에 이뤄진다.
    - 예외 발생시 컴파일 X (class 파일이 생성 X)
    - 엄격한 예외, 형식을 매우 중시
    - 예외가 발생하든 안하든 무조건 예외 처리
    
![image](https://github.com/somi9954/Java/assets/137499604/40e77baf-ef3c-44d6-854b-c4e5fb8fe11e)


    
예외를 발생 시키는 방법 → 예외 던지기(Throwable를 상속 받은 클래스만)
    
throw 예외 객체 → 예외 발생
    
⇒ 예외는 던질수 있는 클래스(Throwable 하위 클래스만 가능), 던지기(throw)를 해야 발생
    
- **Exception**
    - RuntimeException 상속받은 예외
    - 예) ArtithmethicException
        ↳  NullPointerException
           → 참조 변수에 값이 null 인 경우 메서드 호출시 발생
    
    - 예외가 발생 할 수 있더라도 컴파일 O → class 파일이 생성
    - 예외 확인이 실행중(Runtime)에 이뤄진다.
    - 엄격한 예외, 형식을 매우 중시한다.
    
- 다음 그림은 Exception 하위 클래스 중 사용 빈도가 높은 클래스 위주로 계층도를 표현한 것 입니다.
    
![image](https://github.com/somi9954/Java/assets/137499604/691a7a2c-6d30-4a8a-bb59-a1faa1ba3018)


- Exception 클래스 하위에는 이 외에도 많은 클래스가 있습니다. 계층도에서 IOException 클래스는 입출력에 대한 예외를 처리하고, RuntimeException은 프로그램 실행 중 발생할 수 있는 오류에 대한 예외를 처리합니다.
- 이클립스 같은 개발환경에서는 예외가 발생하면 대부분 처리하라는 컴파일 오류 메세지를 띄웁니다. 곧 배우게될 try ~ catch문을 사용하여 예외 처리를 해야 합니다.
- Exception 하위 클래스 중 **RuntimeException**은 try ~ catch문을 사용하여 **예외 처리를 하지 않아도 컴파일 오류가 나지 않습니다**. 곧 배우게 될 예외 전가도 처리하지 않아도 컴파일 오류가 발생하지 않습니다.
- 예를 들어 RuntimeException 하위 클래스 중 ArithmeticException은 산술 연산 중 발생할 수 있는 예외, 즉 '0'으로 숫자 나누기와 같은 경우 발생하는 예외 입니다. 이러한 **컴파일러에 의해 체크되지 않는 예외는 프로그래머가 알아서 처리해야 하므로 주의해야 합니다.**

<aside>
💡 NullPointerException : 객체는 정의가 되었는데 실제 메모리에 생성이 되지 않았을 경우 예외 발생
NumberFormetException : 잘못된 문자열을 숫자로 형 변환할때 예외 발생 (숫자 형태’111’의 문자열은 정수 타입으로 변환할 수 있으나 문자가 포함되거나 실수 형태 ‘11.11’의 문자열은 변환할 수 없다.
ArrayIndexOutOfBoundsException : 배열에서 인덱스(Index) 범위를 초과해 사용할 때 예외 발생
ArithmeticException : 0으로 나누기와 같은 부적절한 산술 연산을 수행할 때 발생.
IndexOutOfBoundsException : 배열, 벡터 등에서 범위를 벗어난 인덱스를 사용할 때 발생.

</aside>

|  | Checked Exception | Unchecked Exception |
| --- | --- | --- |
| 처리여부 | 반드시 예외 처리 필요 | 명시적 처리 강제하지 않음 |
| 확인시점 | 컴파일 단계  | 실행 중 단계 |
| 예외발생시 트랜잭션 | 롤백하지 않음 | 롤백함 |
| 
대표 예외 | 
IOExeption
SQLException | NullPointerException
LLLegal ArgumentException
IndexOutOfBoundException
SystemException |
- **RuntimeException을 중간에 상속 받은 예외 클래스**
    - Runtime : 실행
    예) java.lang.ArithmethicException : 0으로 나눌때 발생
    - 예외가 발생하더라도 컴파일 O
    - class 파일 생성 예외의 체크는 실행 중 체크, 실행이 되려면? class 파일 필요(컴파일은 된다...)
    - 유연한 예외, 형식은 X

참고)

java.exe →자바 class를 실행
javac.exe → java 파일 → class 파일로 컴파일

예외가 발생하면 프로그램 중단! -> 프로그램 중단을 막기 위한 조치
- 예외처리의 목적 : 예외가 발생시 적절한 조치 -> 서비스 중단을 막는 것

---

### 예외 처리하기

예외처리란 프로그램 실행 시 발생할 수 있는 예기치 못한 예외의 발생에 대비한 코드를 작성하는 것이며, 예외처리의 목적은 예외의 발생으로 인한 실행 중인 프로그램의 갑작스런 비정상 종료를 막고, 정상적인 실행상태를 유지할 수 있도록 하는 것이다.

자바에서 예외가 발생되었을 때 처리과정은 다음과 같다.


![image](https://github.com/somi9954/Java/assets/137499604/dfd31f1d-15f3-4a22-bd02-56c20c41761b)


위의 그림과 같이 예외가 발생되면 시스템(JVM)에서 분석하여 예외 클래스 중 알맞은 것을 발생시키고 발생 지점으로 던지게 된다. 발생한 예외를 처리하지 못하면 프로그램은 비정상적으로 종료되며, 처리되지 못한 예외(uncaught exception)은 JVM의 ‘예외처리기(UncaughtExceptionHandler)’가 받아서 예외의 원인을 화면에 출력한다. 넘어온 예외를 처리해 프로그램을 비정상으로 종료되지 않고, 구동할수 있어야 한다.

### 예외 처리하기

1. **try~ catch 문**

예외처리를 하기 위해서는 try-catch문을 사용하며 그 구조는 다음과 같다.

```java
try {
// 예외가 발생할 가능성이 있는 코드
} catch (처리할 예외 클래스 e) {
// 예외에 대한 적절한 처리
}
```

- try 블록에는 **예외가 발생할 가능성이 있는 코드를 작성**한다.
- try 블록 안에 예외가 발생하면 바로 catch 블록이 수행된다.
- catch문의 괄호()안에 쓰는 예외 타입은 예외 상황에 따라 달라진다.
- 다양한 예외가 발생할 수 있는 경우 여러개의 catch 블록을 설정할 수 있다.

```
package day11.exception;

public class ArrayExceptionHandling {
	public static void main(String[] args) {
		int[] arr = new int[5];

		try {
			// 예외가 발생할 수 있으므로 try 블록에 작성
			for (int i = 0; i <= 5; i++) {
				arr[i] = i;
				System.out.println(arr[i]);
			}
		} catch (ArrayIndexOutOfBoundsException e) {
			// 예외가 발생하면 catch 블록 수행
			System.out.println(e);
			System.out.println("예외처리 부분");
		}
	}
}

실행결과

0
1
2
3
4
java.lang.ArrayIndexOutOfBoundsException: Index 5 out of bounds for length 5
예외처리 부분

```

- 배열에 저장하려는 값의 개수가 배열 범위를 벗어났기 때문에 예외가 발생한 것 입니다.
- 참고로 이 예외는 **RuntimeException의 하위 클래스**인 ArrayIndexOutOfBoundsException으로 처리하는에, 이 클래스는 **예외처리를 하지 않아도 컴파일 오류가 나지 않습니다.**
- 따라서 프로그래머가 직접 예외 처리를 하지 않으면 예외가 잡히지 않아서 예외가 발생하는 순간(이 예제에서는 i가 5가 되는 순간) 프로그램이 갑자기 멈춥니다. 그러므로 예외가 발생한 순간 프로그램이 비정상 종료되지 않도록 예외처리를 해주어야 합니다.
- **예외 처리는 프로그램이 비정상 종료되는 것을 방지할 수 있으므로 매주 중요**합니다.

### 컴파일러에 의해 예외가 처리되는 경우

- 자바에서 제공하는 많은 예외 클래스들은 컴파일러에 의해 처리됩니다. 이런 경우 자바에서는 예외 처리를 하지 않으면 컴파일 오류가 계속 남습니다.
- 컴파일오류가 발생하므로 적절한 예외처리가 이뤄지지 않는다면 컴파일이 발생하지 않아 실행되지 않습니다.

```java
package day11.exception;

import java.io.FileInputStream;
import java.io.FileNotFoundException;

public class ExceptionHandling1 {
	public static void main(String[] args) {
		try {
			FileInputStream fis = new FileInputStream("a.txt");
		} catch (FileNotFoundException e) {
			System.out.println(e); // 예외 클래스의 toString() 메서드 호출
		}

		System.out.println("여기도 수행됩니다."); // 정상 출력
	}
}

실행 결과

java.io.FileNotFoundException: a.txt (지정된 파일을 찾을 수 없습니다)
여기도 수행됩니다.

```

> 예외 처리를 한다고 해서 프로그램의 예외 상황 자체를 막을 수는 없습니다. 하지만 예외 처리를 하면 예외 상황을 알려 주는 메시지를 볼 수 있고, 프로그램이 비정상 종료되지 않고 계속 수행되도록 만들 수 있습니다.
> 

1. **메서드에 예외 선언하기** 
- 메서드에 예외를 선언하려면 메서드의 선언부에 키워드 throws를 사용해서 메서드 내에서 발생할 수 있는 예외를 적어주기만 하면 된다. 그리고 예외가 여러 개일 경우에는 쉼표(,)로 구분한다.

```java
void method() throws Exception1, Exception2, ... ExceptionN {
  //메서드의 내용
}
```

<aside>
💡 예외를 발생시키는 키워드 throw와 예외를 메서드에 선언할 때 쓰이는 throws를 잘 구별해야 한다.

</aside>

- 최고 조상인 Exception 클래스를 메서드에 선언하면 이 메서드는 모든 종류의 예외가 발생할 가능성이 있다.  Exception 클래스를 메서드에 선언하면 이 예외뿐만이 아니라 그 자손타입의 예외까지도 발생할 수 있다는점에 유의 해야한다.
- 메서드의 선언부에 예외를 선언함으로써 메서드를 사용하려는 사람이 메서드의 선언부를 보았을 때 이 메서드를 사용하기 위해서는 어떤 예외들이 처리되어져야 하는지 알수 있다.
- 자바에서는 메서드를 작성할 때 메서드 내에서 발생한 가능성이 있는 예외를 메서드의 선언부에 명시하여 이 메서드를 사용하는 쪽에서는 이에 대한 처리를 하도록 강요하기 때문에 견고한 프로그램 코드를 작성할 수 있드록 도와준다.

```java
class Ex8_9 {
	public static void main(String[] args) throws Exception {
		method1();	 // 같은 클래스내의 static멤버이므로 객체생성없이 직접 호출가능.
  	}	// main메서드의 끝

	static void method1() throws Exception {
		method2();
	}	// method1의 끝

	static void method2() throws Exception {
		throw new Exception();
	}	// method2의 끝
```

![image](https://github.com/somi9954/Java/assets/137499604/f0cf8513-92f6-4889-95f2-f10f2d911137)


- 위의 실행결과를 보면 프로그램의 실행도중  java.lang.Exception이 발생하여 비정상적으로 종료되었다는 것과 예외가 발생했을때 호출스택의 내용을 알 수 있다.
    
     1 ) 예외가 발생했을 때, 모두 3개의 메서드(main, method1, method2)가 호출 스택에 있었으며,
    
     2 ) 예외가 발생한 곳은 제일 윗줄에 있는 method2() 라는 것과
    
     3 ) main 메서드가 method1(), 그리고 method1()은 method2()를 호출했다는 것을 알 수 있다.  
    
- 위의 예제를 보면, method2()에서 ‘throw new Exception();’ 문장에 의해 예외가 강제적으로 발생하였으나 try-catch문으로 예외처리를 해주지 않았으므로 method2()는 종료되면서 예외를 자신을 호출한 method1()에게 넘겨준다. method1()에서도 역시 예외처리를 해주지 않았으므로 종료되면서 main메서드에게 예외를 넘겨준다.
- 그러나 main 메서드에서 조차 예외처리를 해주지 않았으므로 main메서드가 종료되어 프로그램이 예외로 인해 비정상적으로 종료되는 것이다.
- 예외가 발생한 메서드에서 예외처리를 하지 않고 자신을 호출한 메서드에게 예외를 넘겨줄 수는 있지만 이것으로 예외가 처리된 것은 아니고 예외를 단순히 전달만 하는 것이다. 결국 어느 한곳에서는 반드시 try-catch문으로 예외처리를 해주어야한다.

```java
	public static void main(String[] args) throws Exception {
		method1();	 // 같은 클래스내의 static멤버이므로 객체생성없이 직접 호출가능.
  	}	// main메서드의 끝

```

- 예외가 선언되어 있으면 Exception과 같은 체크드(chacked) 예외를 try-catch문으로 처리 하지 않아도 컴파일 에러가 발생하지 않는다.

**예외 발생시 문제 해결을 위한 가장 중요한 내용 - 오류 발생의 원인, 정보**
Throwable : 예외의 정보를 확인하는 다양한 메서드가 정의
Throwable
  ↳  Methods String getMessage() :  발생한 예외 클래스의 인스턴스에 저장된 메세지를 얻을 수 있다.

Throwable
  ↳  Methods void printStackTrace() : 예외발생 당시의 호출스택(Call Stack)에 있었던 메서드의 정보와 예외 메세지를 화면에 출력한다.

**멀티 chach블럭** 

- JDK1.7부터 여러 catch블럭을 ‘|’ 기호를 이용해서 하나의 catch 블럭으로  합칠 수 있게 되었으며 이를 멀티 catch 블럭이라고 한다. 멀티 catch블럭을 이용하면 중복된 코드를 줄일 수 있다 ‘|’ 기호로 연결할 수 있는 예외 클래스이 개수에는 제한이 없다.
- 만일 멀티 catch 블럭의 ‘|’기호로 연결된 예외 클래스가 조상과 자손의 관계에 있다면 컴파일 에러가 발생된다.
- 멀티 catch 블럭은 하나의 catch 블럭으로 여러 예외처리를 처리하는 것이기 때문에, 발생한 예외를 멀티 catch 블럭을 처리하게 되었을 때 멀티 catch 블럭 내에서는 실제로 어떤 예외가 발생한 것인지 알 수 없다.

1. **try-catch-finally문**
- try 블록이 수행되면 finally 블록은 어떤 경우에도 반드시 실행됩니다.
- try나 catch에 return문이 있어도 수행됩니다.

예외처리를 하기 위해서는 try-catch-finally문을 사용하며 그 구조는 다음과 같다.

```java
try {
	예외가 발생할 수 있는 부분
} catch (처리할 예외 타입 e) {
	예외를 처리하는 부분
} finally {
	try, catch 구문 종료 후 실행 되는 경우 항상 수행되는 부분
}
```

```java
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

public class ExceptionHandling2 {
	public static void main(String[] args) {
		FileInputStream fis = null;

		try {
			fis = new FileInputStream("a.txt");
		} catch (FileNotFoundException e) {
			System.out.println(e);
			return;
		} finally {
			if (fis != null) {
				try {
					fis.close();  // 파일 입력 스트림 닫기
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
			System.out.println("항상 수행됩니다.");
		}
		System.out.println("여기도 수행됩니다.");
	}
}

실행결과

java.io.FileNotFoundException: a.txt (지정된 파일을 찾을 수 없습니다)
항상 수행됩니다.

```

- 프로그램에서 사용항 리소스는 프로그램이 종료되면 자동으로 해제됩니다. 예를 들어 네트워크가 연결되었을 경우에 채팅 프로그램이 종료될 때 연결도 닫힙니다.
- 하지만 끝나지 않고 계속 수행되는 서비스 같은 경우에 리소스를 여러 번 반복해서 열기만 하고 닫지 않는다면 문제가 발생합니다. **시스템에서 허용하는 자원은 한계가 있습니다.**
- 사용한 시스템 리소스는 사용 후 반드시 close() 메서드로 닫아 주어야 합니다.
- 입력받은 파일이 없는 경우에 대해 try - catch 문을 사용해 FileNotFoundException예외 처리를 하였습니다. 프로그램을 실행하면 a.txt 파일이 없으므로 예외가 발생하여 catch 블록이 수행될 것 입니다.
- 예외를 출력하고 강제로 return을 해보았지만 **return문과 상관 없이 finally 블록이 수행**되어 '항상 수행됩니다.' 문장이 출력 됩니다.
- 파일 접근을 위해 열린 리소스는 **예외 발생과 상관없이 항상 닫혀야 하므로 finally 블록에 파일 리소스를 닫는 코드를 구현**하였습니다.

1. **try-with-resources문**
- 시스템 리소스를 사용하고 해제하는 코드는 다소 복잡합니다.
- JDK1.7 부터 try-with-resources문을 제공하여 close() 메서드를 명시적으로 호출하지 않아도 try 블록 내에서 열린 리소스를 자동으로 닫도록 만들 수 있습니다.
- try-with-resources 문법을 사용하려면 해당 리소스가 **AutoCloseable 인터페이스를 구현**해야 합니다.
- AutoCloseable 인터페이스에는 close() 메서드가 있고 이를 구현한 클래스는 close()를 명시적으로 호출하지 않아도 close() 메서드 부분이 호출됩니다.

### FileInputStream의 JavaDoc 예시

![image](https://github.com/somi9954/Java/assets/137499604/0cb00dbe-f619-48b0-8ecc-6d654ebd5eaf)

- FileInputStream 클래스는 Closeable과 AutoCloseable 인터페이스를 구현했습니다.
- JDK1.7부터는 try-with-resources 문법을 사용하면 FileInputStream을 사용할 때 close()를 명시적으로 호출하지 않아도 정상적인 경우와 예외가 발생한 경우 모두 close()메서드가 호출됩니다.
- FileInputStream 이외에 네트워크(Socket)와 데이터베이스(Connection) 관련 클래스도 AutoCloseable 인터페이스를 구현하고 있습니다.

> AutoCloseable 인터페이스를 구현한 클래스가 무엇이 있는지 궁금하다면 JavaDoc에서 AutoCloseable Interface를 찾아보세요.
> 

### day11/exception/AutoCloseObj.java

```java
package day11.exception;

public class AutoCloseObj implements AutoCloseable {
	@Override
	public void close() throws Exception {
		System.out.println("리소스가 close() 되었습니다.");
	}
}

```

- AutoCloseable 인터페이스는 반드시 close() 메서드를 구현해야 합니다.

### day11/exception/AutoCloseTest.java

```java
package day11.exception;

public class AutoCloseTest {
	public static void main(String[] args) {
		try (AutoCloseObj obj = new AutoCloseObj()) { // 사용할 리소스 선언

		} catch(Exception e) {
			System.out.println("예외 부분 입니다.");
		}
	}
}

실행결과

리소스가 close() 되었습니다.

```

- try-with-resources문을 사용할 때 try문의 괄호() 안에 리소스를 선언합니다.
- 이 예제는 예외가 발생하지 않고 정상 종료 되는데 출력 결과를 보면 close() 메서드가 호출되어 **리소스가 close() 되었습니다.** 문장이 출력 됩니다.
- 리소스를 여러개 생성해야 한다면 세미 콜론(;)으로 구분합니다.

```java
try(A a = new A(); B b = new B()) {
	...
} catch(Exception e) {
	...
}

```

### day11/exception/AutoCloseObjTest.java

```java
package day11.exception;

public class AutoCloseObjTest {
	public static void main(String[] args) {
		try (AutoCloseObj obj = new AutoCloseObj()) { // 사용할 리소스 선언
			throw new Exception(); // 강제 예외 발생
		} catch(Exception e) {
			System.out.println("예외 부분 입니다.");
		}
	}
}

실행결과

리소스가 close() 되었습니다.
예외 부분 입니다.

```

- 강제로 예외를 발생시키면 catch 블록이 수행됩니다.
- 출력 결과를 보면 리소스의 close() 메서드가 먼저 호출되고 예외 블록 부분이 수행되는 것을 알 수 있습니다.
- 이처럼 try-with-resources문을 사용하면 close() 메서드를 명시적으로 호출하지 않아도 정상 종료된 경우와 예외가 발생한 경우 모두 리소스가 잘 해제 됩니다.
- 자바 9버전에는 응용된 try -with-resources문이 나왔다.

https://countryxide.tistory.com/87

- try → chach를 써도 되고 안써도 됨 아니면  finally로 많이 사용한다.

---

### 예외 처리 미루기

**예외 처리를 미루는 throws 사용하기**

- 예외를 해당 메서드에서 처리하지 않고 미룬 후 메서드를 호출하여 사용하는 부분에서 예외를 처리하는 방법
- 연산자 new를 이용해서 발생 시키려는 예외 클래스의 객체를 만든 다음
    ↳   Exception e = new Exception(”고의로 발생시켰음”);

- 키워드 throw를 이용해서 예외를 발생 시킨다.
    ↳  throw e;

```java
class Ex8_6 {
	public static void main(String args[]) {
		try {
			Exception e = new Exception("고의로 발생시켰음.");
			throw e;	 // 예외를 발생시킴
		//  throw new Exception("고의로 발생시켰음."); 위의 두줄을 한줄로 줄여 쓸 수 있다.

		} catch (Exception e)	{
			System.out.println("에러 메시지 : " + e.getMessage());
			e.printStackTrace();
		}
		System.out.println("프로그램이 정상 종료되었음.");
	}
}
출력값 
에러 메세지 : 고의로 발생시켰음.
java.lang.Exception : 고의로 발생시켰음
		 at Ex8_6.main(Ex8_6.java:4)
프로그램이 정상 종료 되었음.
```

Exception인스턴스를 생성할 때, 생성자에 String을 넣어주면 이 String이 Exception인스턴스에 메세지로 저장된다. 이 메세지는 getMessage()를 이용해서 얻을 수 있다.

### throws를 활용하여 예외처리 미루기

- 예외를 처리하지 않고 미룬다고 선언하면, 그 메서드를 호출하여 사용하는 부분에서 예외 처리를 해야 합니다.

![image](https://github.com/somi9954/Java/assets/137499604/a8794852-ae7d-4348-a301-9a410d0f7672)

![image](https://github.com/somi9954/Java/assets/137499604/12c5b6cc-e273-4a9f-bfda-5aeb676e4dab)


- **Add throws declaration**
    - main() 함수 선언 부분에 throws FileNotFoundException, ClassNotFoundException을 추가하고 예외 처리를 미룬다는 뜻 입니다.
    - main() 함수에서 미룬 예외 처리는 main() 함수를 호출하는 자바 가상 머신으로 보내집니다.즉, 예외를 처리하는 것이 아니라 대부분의 프로그램이 비정상 종료 됩니다.
- **Surround with try/multi-catch** - 여러 예외를 한꺼번에 처리하기
    
    ```java
     public static void main(String[] args) {
     	ThrowsException test = new ThrowsException();
     	try {
     		test.loadClass("a.txt", "java.lang.String");
     	} catch (FileNotFoundException | ClassNotFoundException e) {
     		// TODO Auto-generated catch block
     		e.printStackTrace();
     	}
     }
    
    ```
    
- **Surround with try/catch** - 예외를 상황마다 처리하기
    
    ```java
     ...
     public static void main(String[] args) {
     	ThrowsException test = new ThrowsException();
     	try {
     		test.loadClass("a.txt", "java.lang.String");
     	} catch (FileNotFoundException e) {
     		// TODO Auto-generated catch block
     		e.printStackTrace();
     	} catch (ClassNotFoundException e) {
     		// TODO Auto-generated catch block
     		e.printStackTrace();
     	}
     }
     ...
    
    ```
    
- 예외가 발생한 메서드에서 그 예외를 바로 처리할 것인지, 아니면 미루어서 그 메서드를 호출하여 사용하는 부분에서 처리할 것인지는 만들고자 하는 프로그램 상황에 따라 다를 수 있습니다.
- 만약 어떤 메서드가 다른 여러 코드에서 호출되어 사용된다면 메서드를 호출하는 부분에서 예외처리를 하도록 미루는 것이 합리적입니다.

---

### 다중 예외 처리

• 어떤 예외가 발생할지 미리 알수 없지만 모든 예외 상황을 처리하고자 한다면 맨 마지막 부분에 Exception 클래스를 활용하여 catch 블록을 추가합니다.

```java
package day11.exception;

import java.io.FileInputStream;
import java.io.FileNotFoundException;

public class ThrowsException {
	public Class loadClass(String fileName, String className) throws FileNotFoundException, ClassNotFoundException {
		FileInputStream fis = new FileInputStream(fileName); // FileNotFoundException 발생 가능
		Class c = Class.forName(className); // ClassNotFoundException 발생 가능
		return c;
	}
	public static void main(String[] args) {
		ThrowsException test = new ThrowsException();
		try {
			test.loadClass("a.txt", "java.lang.String");
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (ClassNotFoundException e) {
			e.printStackTrace();
		} catch (Exception e) { // Exception  클래스로 그 외 예외 상황 처리
			e.printStackTrace();
		}
	}
}

```

- Exception 클래스는 모든 예외 클래스의 최상위 클래스 입니다. 따라서 다른 catch 블록에서 선언한 것 이외의 예외가 발생하더라도 Exception 클래스로 자동 형 변환 됩니다(다형성).
- 가장 처음 Exception이 catch 구간에 있다면 모든 예외가 이 구간으로 유입이 되어 적절한 처리가 되지 않습니다. 따라서 기본 예외 처리를 하는 **Exception 클래스 블록은 여러 예외 처리 블록의 가장 아래 놓여야 합니다.**

```java
package section14;
import java.util.InputMismatchException;
import java.util.Scanner;

public class EX14_06 {
	public static void main(String[] args) {
		Scanner scan = new Scanner(System.in);
		
		try {
			int[] cards = {4, 5, 1, 2, 7, 8};
			System.out.println("몇 번째 카드를 뽑으시겠습니까? >>");
			
			int cardIndex = scan.nextInt();
			System.out.println("뽑은 카드 번호는 : " + cards[cardIndex]);
			
		} catch(InputMismatchException e) {
			System.out.println("잘못 입력하셨습니다. 숫자만 가능합니다.");
		}
		
		System.out.println("프로그램 종료");
		scan.close();
	}
}
```

- 카드의 번호를 입력할 때 숫자가 아닌 문자를 입력할 경우 예외 처리도 정상적으로 가능하다. 그러나 배열의 길이가 7개, 즉 배열의 index가 6까지 있는데 실수로 더 많은 번호를 입력하게 된다면 배열의 위치가 잘못되어 예외가 발생하게 된다. 해당 처리가 되질 않아 프로그램이 비정상으로 동작하게 된다.
- 다음은 모든 예외가 정상 처리 된 경우의 예제이다.

```java
package section14;
import java.util.InputMismatchException;
import java.util.Scanner;

public class EX14_07 {
	public static void main(String[] args) {
		
		Scanner scan = new Scanner(System.in);
		
		try {
			int[] cards = {4, 5, 1, 2, 7, 8};
			System.out.println("몇 번째 카드를 뽑으시겠습니까? >>");
			
			int cardIndex = scan.nextInt();
			System.out.println("뽑은 카드 번호는 :" + cards[cardIndex]);
			
		} catch(InputMismatchException e) {
			System.out.println("잘못 입력하셨습니다. 숫자만 가능합니다.");
		} catch(ArrayIndexOutOfBoundsException e) {
			System.out.println("해당 번호의 카드는 없습니다.");
		}
		
		System.out.println("프로그램 종료");
		scan.close();
	}
}

출력값 
몇 번째 카드를 뽑으시겠습니까? >>
  11
해당 번호의 카드는 없습니다.
프로그램 종료 
```

- 위와 같이 예외를 다중 처리하여 프로그램을 구성하면 코드에서 발생하는 다양한 예외를 처리할 수 있다. 따라서 보다 안정적인 프로그래밍이 가능하다.

---

### 사용자 정의 예외

- 문법적인 예외가 발생하지 않았더라도, 프로그램의 규칙에 맞지 않거나 흐름에 문제가 생기면 사용자가 직접 예외를 발생 시킬 수 있다.
- 목적에 따라 공통기능을 지니는 예외 처리도 필요하기 때문에 개발자가 직접 예외를  생성하여 처리한다.
- 사용자 정의 예외 클래스를 구현할 때는 기존 JDK에서 제공하는 예외 클래스 중 가장 유사한 클래스를 상속받는 것이 좋습니다.
- 유사한 예외 클래스를 잘 모르겠다면 **가장 상위 클래스인 Exception 클래스**를 상속받으시면 됩니다.

```java
package section14;

public class InputErrorException extends Exception { //Exception 객체를 상속받습니다.
	private String message;
	public InputErrorException(String message) {  //객체를 선언할때 예외 메세지를 입력 받도록 한다.
		this.message = message;
	}
	
	@Override
	public String getMessage() {  //Exception이 지닌 getMessage() 메서드를 오버라이드하여 재정의한다. 입력받은 메세지를 리턴한다.
		return this.message;
	}
}
```

- 위 코드는 Exception 클래스에서 상속받아 구현했습니다.
- 예외 상황 메세지를 생성자에 입력 받습니다.
- Exception 클래스에서 메세지 생성자, 멤버 변수와 메서드를 이미 제공하고 있으므로 super(message)를 사용하여 메시지를 설정합니다.
- 나중에 getMessage() 메서드를 호출하면 메시지 내용을 볼 수 있습니다.

```java
package section14;
import java.util.Scanner;

public class EX14_12 {
	public static void main(String[] args) {
		// 스캐너 생성
		Scanner scan = new Scanner(System.in);
		try {
			// 나이 입력
			System.out.print("당신의 나이를 입력하세요 >>");
			int age = scan.nextInt();
			
			if(age < 0) {
				// 1살 미만인 경우 입력 실패
				throw new InputErrorException("입력이 잘못되었습니다."); //개발자가 만든 InputErrorException을 임의로 예외 발생 시킨다.
			}
			
			if(age > 19) {
				System.out.println("성인입니다.");
			} else if(age > 13) {
				System.out.println("청소년입니다.");
			} else if(age > 6) {
				System.out.println("어린이입니다.");
			} else {
				System.out.println("아동입니다.");
			}
		} catch(InputErrorException e) {   // 발생한 예외를 처리한다.
			System.out.println(e.getMessage());
		} finally {
			if(scan != null) {
				scan.close();
			}
		}
	}
}

출력값
당신의 나이를 입력하세요 >> -1
입력이 잘못되었습니다.
```

- 여기에서 발생하는 예외는 자바에서 제공하는 예외가 아니므로 예외 클래스를 직접 생성하여 예외를 발생시켜야 합니다.
- 예외 메시지를 생성자에 넣어 예외 클래스를 생성한 후 **throw문으로 직접 예외를 발생**시킵니다.
