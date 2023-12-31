# 쓰레드

## 프로세스와 쓰레드

- 프로세스 : 실행 중인 프로그램이다. 프로그램을 실행하려면 OS로 부터 실행에 필요한 자원(메모리) 할당 받아 프로세스가 된다.
- 프로세스는 프로그램을 수행하는 데 필요한 **데이터**와 **메모리**등의 자원 그리고 **쓰레드**로 구성되어 있다.
- 프로세스의 자원을 이용해서 실제로 작업을 수행하는 것이 **쓰레드**(메모리+ 작업대(공간))이다.
- 모든 프로세스에는 최소한 하나 이상의 쓰레드가 존재하며, 둘 이상의 쓰레드를 가진 프로세스를 **멀티쓰레드 프로세스**(multi-threaded process)라고 한다.
- 하나의 프로세스가 가질 수 있는 쓰레드의 개수는 제한되어 있지 않으나 쓰레드가 작업을 수행하는데 **개별적인 메모리 공간**(호출 스택)을 필요로 하기 때문에 **프로세스의 메모리 한계에 따라 생성할 수 있는 쓰레드의 수가 결정**된다.

<img src="https://github.com/somi9954/Java/assets/137499604/6bc61d58-0022-4f33-8632-f366d894f99f" width="500">


## 멀티쓰레딩

- 멀티쓰레딩은 하나의 프로세스내에서 여러 쓰레드가 동시에 작업을 수행하는 것이다.

1. 멀티쓰레딩의 장점
- CPU 사용율을 향상
- 자원의 효율성
- 사용자의 경험(응답성) 향상
- 작업이 분리되어 코드가 간결해진다.
1. 멀티쓰레딩의 단점
    - 하나의 자원을 서로 공유 -> 동시성(동기화(synchronization)**)** 문제 발생

## 쓰레드의 구현과 실행

1. 구현
    - Thread클래스를 상속
    java.lang.Thread 클래스
    
    ```java
    class MyThread extends Thread{
    	public void run() { /*작업내용*/ } //Thread 클래스의 run()을 오버라이딩
    }
    ```
    
    - Runnable인터페이스를 구현
        
        ```java
        class MyThread implements Runnable{
        	public void run() { /*작업내용*/ } 
        //Runnable 인터페이스의 run()을 오버라이딩
        }
        ```
        
    - Runnable 인터페이스는 오로지 run만 정의되어 있는 간단한 인터페이스 이다.
    
    ```java
    public interface Runnable {
    	public abstract void run();
    }
    ```
    
    참고)
    static Thread.currentThread() : 현재 실행 중인 쓰레드
    
    String getName() :  쓰레드의 이름을 반환한다.
    

## 쓰레드의 실행 - start()

- start()와 run()
- 쓰레드를 생성했다고 해서 자동으로 실행되는 것은 아니다.
- start()를 호출해야만 쓰레드가 실행된다.
- 사실은 start()가 호출되었다고 해서 바로 실행되는 것이 아니라. 일단 실행대기 상태에 있다가 자신의 차례가 되어야 실행된다. 물론 실행대기중인 쓰레드가 하나도 없으면 곧바로 실행상태가 된다.
- 한 번 실행이 종료된 쓰레드는 다시 실행할 수 없다.(즉, 하나의 쓰레드에 대해 start()가 한번만 호출될수 있다.)

> 쓰레드의 실행순서는 OS의 스케줄러가 작성한 스케줄에 의해 결정된다.
> 

```java
ThreadEx1_1 t1 = new ThreadEx1_1();
t1.start();
t1.start(); // IllegalThreadStateException 예외발생

```

### start()와 run()

- main메서드에서 run()을 호출하는 것은 생성된 쓰레드를 실행시키는 것이 아니라 단순히 클래스에 선언된 메서드를 호출하는 것일 뿐이다.
- **main메서드에서 run()을 호출했을 때의 호출스택**

<img src="https://github.com/somi9954/Java/assets/137499604/b6b6440b-ca4e-47ba-8ee6-bdb20847de79" width="450">

1. 반면에 start()는 새로운 쓰레드가 작업을 실행하는데 필요한 호출스택(call stack)을 생성한 다음에 run()을 호출해서, 생성된 호출 스택에 run()이 첫 번째로 올라가게 한다.
2. 모든 쓰레드는 독립적인 작업을 수행하기 위해 자신만의 호출스택을 필요로 하기 때문에, 새로운 쓰레드를 생성하고 실행시킬 때마다 새로운 호출스택이 생성되고 스레드가 종료되면 작업에 사용된 호출스택은 소멸된다.
- **새로운 쓰레드를 생성하고 start()를 호출한 후 호출스택의 변화**

<img src="https://github.com/somi9954/Java/assets/137499604/138f5d76-ce3b-4ae7-923d-31ada83512d6" width="450">


1. main() 메서드에서 쓰레드의 start()를 호출한다.
2. start()는 새로운 쓰레드를 생성하고 쓰레드가 작업하는데 사용될 호출 스택을 생성한다.
3. 새로 생성된 호출스택에 run()이 호출되어, 쓰레드가 독립된 공간에서 작업을 수행한다.
4. 이제는 호출 스택이 2개이므로 스케줄러가 정한 순서에 의해서 번갈아가며 실행된다.
- 쓰레드가 둘 이상일 때는 호출스택의 최상위에 있는 메서드일지라도 대기상태에 있을 수 있다.
- 스케줄러는 실행대기중인 쓰레드들의 우선순위를 고려하여 실행순서와 실행시간을 결정하고, 각 쓰레드들은 작성된 스케줄에 따라 자신의 순서가 되면 지정된 시간동안 작업을 수행한다.
- 이 때 주어진 시간동안 작업을 마치지 못한 쓰레드는 다시 자신의 차례가 돌아올 때까지 대기상태로 있게 된다.
- 작업을 마친 쓰레드, 즉 run()은 수행이 종료된 쓰레드는 호출스택이 모두 비워지면서 이 쓰레드가 사용하던 호출스택은 사라진다.
- 이는 자바프로그램을 실행하면 호출스택이 생성되고 main메서드가 처음으로 호출되고, main메서드가 종료되면 호출스택이 비워지면서 프로그램도 종료되는 것과 같다.

### main 쓰레드

- main메서드의 작업을 수행하는 것도 쓰레드이며, 이를 main쓰레드라고 한다.
- main메서드가 수행를 마쳤다하더라도 다른 쓰레드가 아직 작업을 마치지 않은 상태라면 프로그램이 종료되지 않는다.
- **실행중인 사용자 쓰레드가 하나도 없을 때 프로그램은 종료된다.**

day17/ThreadEx2.java

```java
package day17;

class ThreadEx2_1 extends Thread {
	public void run() {
		throwException();
	}

	public void throwException() {
		try {
			throw new Exception();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

public class ThreadEx2 {
	public static void main(String[] args) throws Exception {
		ThreadEx2_1 t1 = new ThreadEx2_1();
		t1.start();
	}
}

실행결과
java.lang.Exception
	at day17.ThreadEx2_1.throwException(ThreadEx2.java:10)
	at day17.ThreadEx2_1.run(ThreadEx2.java:5)

```

- 호출스택의 첫 번쨰 메서드가 main 메서드가 아니라 run메서드이다.
- 한 쓰레드가 예외가 발생해서 종료되어도 다른 쓰레드의 실행에는 영향을 미치지 않는다.
- main쓰레드 호출스택이 없는 이유는 main쓰레드가 종료되었기 때문이다.

![https://raw.githubusercontent.com/yonggyo1125/curriculum300H/main/1.JAVA(84%EC%8B%9C%EA%B0%84)/17%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%93%B0%EB%A0%88%EB%93%9C/images/start_%EC%8B%A4%ED%96%89.png](https://raw.githubusercontent.com/yonggyo1125/curriculum300H/main/1.JAVA(84%EC%8B%9C%EA%B0%84)/17%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%93%B0%EB%A0%88%EB%93%9C/images/start_%EC%8B%A4%ED%96%89.png)

day17/ThreadEx3.java

```java
package day17;

class ThreadEx3_1 extends Thread {
	public void run() {
		throwException();
	}

	public void throwException() {
		try {
			throw new Exception();
		} catch (Exception e) {
			e.printStackTrace();
		}
	}
}

public class ThreadEx3 {
	public static void main(String[] args) throws Exception {
		ThreadEx3_1 t1 = new ThreadEx3_1();
		t1.run();
	}
}

실행결과
java.lang.Exception
	at day17.ThreadEx3_1.throwException(ThreadEx3.java:11)
	at day17.ThreadEx3_1.run(ThreadEx3.java:6)
	at day17.ThreadEx3.main(ThreadEx3.java:21)

```

- 단순히 ThreadEx3_1 클래스의 run()이 호출되었고 쓰레드가 새로 생성되지 않았다.
- main쓰레드의 호출 스택에서 run()이 호출되었고 main메서드가 포함되어 있다.
    
    ![https://raw.githubusercontent.com/yonggyo1125/curriculum300H/main/1.JAVA(84%EC%8B%9C%EA%B0%84)/17%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%93%B0%EB%A0%88%EB%93%9C/images/run_%EC%8B%A4%ED%96%89.png](https://raw.githubusercontent.com/yonggyo1125/curriculum300H/main/1.JAVA(84%EC%8B%9C%EA%B0%84)/17%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%93%B0%EB%A0%88%EB%93%9C/images/run_%EC%8B%A4%ED%96%89.png)
    

## 싱글쓰레드와 멀티쓰레드

- 하나의 쓰레드로 두 작업을 처리하는 경우 한 작업을 마친 후에 다른 작업을 시작한다.
- 두 개의 쓰레드로 작업하는 경우에는 짧은 시간동안 2개의 쓰레드가 번갈아 가면서 작업을 수행해서 동시에 두 작업이 처리되는 것과 같이 느끼게 한다. (시분할 방식)
- 하나의 쓰레드로 두개의 작업을 수행한 시간과 두개의 쓰레드로 두 개의 작업을 수행한 시간은 거의 같다.
- 오히려 두 개의 쓰레드로 작업한 시안이 싱글쓰레드로 작업한 시간보다 더 걸리게 되는데, 쓰레드간의 작업 전환(context switching)에 시간이 걸리기 때문이다.
- 작업 전환을 할 때는 현재 진행 중인 작업의 상태, 다음에 실행할 위치 등의 정보를 저장하고 읽어 오는 시간이 소요된다.
- 단순히 CPU만 사용하는 계산작업이라면 오히려 멀티쓰레드보다 싱글쓰레드로 프로그래밍하는 것이 더 효율적이다.

![image](https://github.com/somi9954/Java/assets/137499604/b42ecedb-6cf9-4c75-8554-1370ef2a2bf7)


> 프로세스 또는 쓰레드간의 작업 전환을 컨텍스트 스위칭(context switching)이라고 한다.
> 

## **쓰레드의 우선순위**

### 쓰레드 우선순위 지정하기

- 싱글 코어 : 정확하게 동작
- 멀티 코어는 : 정확하지 않다.

```java
1~10 : setPriortiy(1~10)
int getPriority() : 쓰레드의 우선순위

MAX_PRIORITY : 10  //최대 우선순위
MIN_PRIORITY : 1     //최소 우선 순위
NORM_PRIORITY : 5  //보통 우선 순위 
```

- 쓰레드가 가질 수 있는 우선순위 범위는 1~10이며 숫자가 높을수록 우선순위가 높다
- 쓰레드의 우선순위는 쓰레드를 생성한 쓰레드로부터 상속받는다.
- main메서드를 수행하는 쓰레드는 우선순위가 5이므로 main메서드내에서 생성하는 쓰레드의 우선순위는 자동적으로 5가 된다.
- 쓰레드의 우선순위는 쓰레드를 실행하기 전에 변경할 수 있다.

```java
package exam02;

public class Ex05 {
    public static void main(String[] args) {
        Thread2 th2 = new Thread2();
        Thread3 th3 = new Thread3();
        th2.setPriority(Thread.MAX_PRIORITY);
        th3.setPriority(Thread.MIN_PRIORITY);

        System.out.println("th2 우선순위 : " + th2.getPriority());
        System.out.println("th3 우선순위 : " + th3.getPriority());
        th2.start();
        th3.start();
    }
}

class Thread2 extends Thread {
    public void run(){
        for (int i = 0; i < 300; i++) {
            System.out.print(new String("-"));
            for (long j = 0; j < 10000000L ; j++);
        }
    }
}

class Thread3 extends Thread {
    public void run(){
        for (int i = 0; i < 300; i++) {
            System.out.print(new String("|"));
            for (long j = 0; j < 10000000L ; j++);
        }
    }
    }
```

<img src="https://github.com/somi9954/Java/assets/137499604/a51bc061-0a17-44d9-b4d6-93b20ffce3b9">


### 쓰레드 그룹(thread group)

- 서로 관련된 쓰레드를 그룹으로 다루기 위한 것
- 모든 쓰레드는 쓰레드 그룹에 소속
- ThreadGroup을 사용해서 생성할 수 있다.

**ThreadGroup의 생성자와 메서드**

| 생성자 / 메서드 | 설명 |
| --- | --- |
| ThreadGroup(String name) | 지정된 이름의 새로운 쓰레드 그룹을 생성 |
| ThreadGroup(ThreadGroup parent, String name) | 지정된 쓰레드 그룹에 포함되는 새로운 쓰레드 그룹을 생성 |
| int activeCount() | 쓰레드 그룹에 포함된 활성상태에 있는 쓰레드의 수를 반환 |
| int activeGroupCount() | 쓰레드 그룹에 포함된 활성상태에 있는 쓰레드 그룹의 수를 반환 |
| void checkAccess() | 현재 실행중인 쓰레드가 쓰레드 그룹을 변경할 권한이 있는지 체크, 만일 궎란이 없다면 SecurityException을 발생시킨다. |
| void destroy() | 쓰레드 그룹과 하위 쓰레드 그룹까지 모두 삭제한다. 단 쓰레드 그룹이나 하위 쓰레드 그룹은 비어있어야 한다. |
| int enumerate(Thread[] list)int enumerate(Thread[] list, boolean recurse)int enumerate(ThreadGroup[] list)int enumerate(ThreadGroup[] list, boolean recurse) | 쓰레드 그룹에 속한 쓰레드 또는 하위 쓰레드 그룹의 목록을 지정된 배열에 담고 그 개수를 반환.두 번째 매개변수인 recurse의 값을 true로 하면 쓰레드 그룹에 속한 하위 쓰레드 그룹에 쓰레드 또는 쓰레드 그룹까지 배열에 담는다. |
| int getMaxPriority() | 쓰레드 그룹의 최대우선순위를 반환 |
| String getName() | 쓰레드 그룹의 이름을 반환 |
| ThreadGroup getParent() | 쓰레드 그룹의 상위 쓰레드그룹을 반환 |
| void interrupt() | 쓰레드 그룹에 속한 모든 쓰레드를 interrupt |
| boolean isDaemon() | 쓰레드 그룹이 데몬 쓰레드그룹인지 확인 |
| boolean isDestoryed() | 쓰레드 그룹이 삭제되었는지 확인 |
| void list() | 쓰레드 그룹에 속한 쓰레드와 하위 쓰레드그룹에 대한 정보를 출력 |
| boolean parentOf(ThreadGroup g) | 지정된 쓰레드 그룹은 상위 쓰레드그룹인지 확인 |
| void setDaemon(boolean daemon) | 쓰레드 그룹을 데몬 쓰레드 그룹으로 설정/해제 |
| void setMaxPriority(int pri) | 쓰레드 그룹의 최대우선순위를 설정 |

```java
Thread(ThreadGroup group, String name)
Thread(ThreadGroup group, Runnable target)
Thread(ThreadGroup group, Runnable target, String name)
Thread(ThreadGroup group, Runnable target, String name, long stackSize)

```

- 모든 쓰레드는 반드시 쓰레드 그룹에 포함되어 있어야 하기 때문에 쓰레드 그룹을 지정하하는 생성자를 사용하지 않은 쓰레드는 기본적으로 자신을 생성한 쓰레드와 같은 그룹에 속하게 된다.
- 자바 애플리케이션이 실행이 되면, JVM은 main과 system이라는 쓰레드 그룹을 만들고 JVM운영에 필요한 쓰레드들을 생성해서 이 쓰레드 그룹을 포함시킨다.
- 예를 들면 main메서드를 수행하는 main이라는 이름의 쓰레드는 main쓰레드 그룹에 속하고, 가비지 컬렉션을 수향하는 Finalizer쓰레드는 system쓰레드 그룹에 속한다.
- 우리가 생성하는 모든 쓰레드 그룹은 main쓰레드 그룹의 하위 쓰레드 그룹이 되며, 쓰레드 그룹을 지정하지 않고 생성한 쓰레드는 자동적으로 main쓰레드 그룹에 속하게 된다.
- 그 외에 Thread의 쓰레드 그룹과 관련된 메서드

```java
ThreadGroup getThreadGroup()  // 쓰레드 자신이 속한 쓰레드 그룹을 반환한다.
void uncaughtException(Thread t, Throwable e)  // 쓰레드 그룹의 쓰레드가 처리되지 않은 예외에 의해 실행이 종료되었을 때, JVM에 의해 이 메서드가 자동적으로 호출된다.

```

```java
package day17;

public class Ex02 {
    public static void main(String[] args) {
        ThreadGroup grp1 = new ThreadGroup("Group1");
        ThreadGroup grp2 = new ThreadGroup("Group2");
        ThreadGroup grp3 = new ThreadGroup(grp1, "SubGroup1");

        Runnable r = () -> {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            }
        };

        grp1.setMaxPriority(1);

        Thread th1 = new Thread(grp1, r, "th1");
        Thread th2 = new Thread(grp2, r, "th2");
        Thread th3 = new Thread(grp3, r, "th3");

        th1.start();
        th2.start();
        th3.start();

        grp1.list();
        grp2.list();
    }
}

실행결과
>>java.lang.ThreadGroup[name=Group1,maxpri=1]
    Thread[#22,th1,1,Group1]
    java.lang.ThreadGroup[name=SubGroup1,maxpri=1]
        Thread[#24,th3,1,SubGroup1]
java.lang.ThreadGroup[name=Group2,maxpri=10]
    Thread[#23,th2,5,Group2]

```

- 새로 생성한 모든 쓰레드 그룹은 main쓰레드 그룹의 하위 쓰레드 그룹으로 포함되어 있다.
- setMaxPriority()는 쓰레드가 쓰레드 그룹에 추가되이 이전에 호출되어야 한다.
- 쓰레드 그룹 grp1의 최대우선순위를 3으로 했기 때문에, 후에 여기에 속하게 된 쓰레드 그룹과 쓰레드가 영향을 받았다.

### 데몬 쓰레드(daemon thread)

- 다른 일반 쓰레드의 보조 쓰레드
- 다른 일반 쓰레드의 작업이 종료 -> 보조 쓰레드도 종료 → 데몬 쓰레드의 존재가 없어진다
- 데몬 쓰레드의 예에는 GC(Garbage Collector), 문서 자동 저장 기능 → 3초마다 문자 저장, 자바 스크립트의 이벤트 루프이 있다.
- 데몬 쓰레드는 무한루프와 조건문을 이용해서 실행 후 대기하고 있다가 특정 조건이 만족되면 작업을 수행하고 다시 대기하도록 작성한다.
- 데몬 쓰레드는 일반 쓰레드의 작성방법과 실행방법이 같다. 다만 쓰레드를 생성한 다음 실행하기 전에 setDaemon(true)를 호출하기만 하면 된다.
- 데몬 쓰레드가 생성한 쓰레드는 자동적으로 데몬 쓰레드가 된다.

```java
boolean isDaemon()  // 쓰레드가 데몬 쓰레드인지 확인한다. 데몬 쓰레드이면 true를 반환한다.
void setDaemon(boolean on) // 쓰레드를 데몬 쓰레드로 또는 사용자 쓰레드로 변경한다. 매개변수 on의 값을 true로 지정하면 데몬 쓰레드가 된다.

```

```java
package exam02;

public class Ex06 {
    public static void main(String[] args) {
        Thread mainTh = Thread.currentThread();
        System.out.println(mainTh.getThreadGroup());

        Thread4 th = new Thread4();
        System.out.println(th.getThreadGroup());

        th.setDaemon(true);
        th.start();

        for (int i = 1; i <= 10 ; i++) {
            System.out.println(i);
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            }
        }
    }
}

class Thread4 extends Thread {
    public void run() {
        while (true) {

            try {
                Thread.sleep(3000);
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            }
            System.out.println("문서 저장 완료!");
        }
    }
}
```

```java
출력값
java.lang.ThreadGroup[name=main,maxpri=10]
java.lang.ThreadGroup[name=main,maxpri=10]
1
2
3
문서 저장 완료!
4
5
6
문서 저장 완료!
7
8
9
문서 저장 완료!
10
```

## 쓰레드의 실행제어

- 쓰레드 프로그래밍이 어려운 이유는 동기화(synchronizaion)와 스케줄링(scheduling)때문이다.
- 효율적인 멀티쓰레드 프로그램을 만들기 위해서는 보다 정교한 스케줄링을 통해 프로세스에게 주어진 시간을 여러 쓰레드가 낭비없이 잘 사용하도록 프로그래밍 해야 한다.

**쓰레드와 스케줄링과 관련된 메서드**

| 메서드 | 설명 |
| --- | --- |
| static void sleep(long millis)static void sleep(long millism int nanos) | 지정된 시간(천분의 일초 단위)동안 쓰레드를 일시정지시킨다. 지정한 시간이 지나고 나면, 자동적으로 다시 실행대기상태가 된다. |
| void join()void join(long millis)void join(long millis, int nanos) | 지정된 시간동안 쓰레드가 실행되도록 한다. 지정된 시간이 지나거나 작업이 종료되면 join()을 호출한 쓰레드로 다시 돌아와 실행을 계속한다. |
| void interrupt() | sleep()이나 join()에 의해 일시정지상태인 쓰레드를 깨워서 실행대기상태로 만든다. 해당 쓰레드에서는 InterruptedException이 발생함으로써 일시정지상태를 벗어나게 된다. |
| void stop() | 쓰레드를 즉시 종료시킨다. |
| void suspend() | 쓰레드를 일시정지시킨다. resume()을 호출하면 다시 실행대기상태가 된다. |
| void resume() | suspend()에 의해 일시정지상태에 있는 쓰레드를 실행대기상태로 만든다. |
| static void yield() | 실행 중에 자신에게 주어진 실행시간을 다른 쓰레드에게 양보(yield)하고 자신은 실행대기 상태가 된다. |

> resume(), stop(), suspend()는 쓰레드를 교착상태(dead-lock)로 만들기 쉽기 때문에 deprecated되었다.
> 

**쓰레드의 상태**

| 상태 | 설명 |
| --- | --- |
| NEW | 쓰레드가 생성되고 아직 start()가 호출되지 않은 상태 |
| RUNNABLE | 실행 중 또는 실행 가능한 상태 |
| BLOCKED | 동기화블럭에 의해서 일시정지된 상태(lock이 풀릴 때까지 기다리는 상태) |
| WAITINGTIMED_WAITING | 쓰레드의 작ㅇ버이 종료되지는 않았지만 실행가능하지 않은(unrunnable) 일시정지 상태. TIMED_WAITING은 일시정지시간이 지정된 경우를 의미한다. |
| TERMINATED | 쓰레드의 작업이 종료된 상태 |

![https://raw.githubusercontent.com/yonggyo1125/curriculum300H/main/1.JAVA(84%EC%8B%9C%EA%B0%84)/17%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%93%B0%EB%A0%88%EB%93%9C/images/%EC%93%B0%EB%A0%88%EB%93%9C%EC%9D%98_%EC%83%81%ED%83%9C.png](https://raw.githubusercontent.com/yonggyo1125/curriculum300H/main/1.JAVA(84%EC%8B%9C%EA%B0%84)/17%EC%9D%BC%EC%B0%A8(3h)%20-%20%EC%93%B0%EB%A0%88%EB%93%9C/images/%EC%93%B0%EB%A0%88%EB%93%9C%EC%9D%98_%EC%83%81%ED%83%9C.png)

1. 쓰레드를 생성하고 start()를 호출하면 바로 실행된느 것이 아니라 실행대기열에 저장되어 자신의 차례가 될 떄까지 기다려야 한다. 실행대기열은 큐(queue)와 같은 구조로 먼저 실행대기열에 들어온 쓰레드가 먼저 실행된다.
2. 실행대기 상태에 있다가 자신의 차례가 되면 실행상태가 된다.
3. 주어진 실행시간이 다 되거나 yield()를 만나면 다시 실행대기상태가 되고 다음 차례의 쓰레드가 실행상태가 된다.
4. 실행 중에 suspend(), sleep(), wait(), join(), I/O block에 의해 일시정지상태가 될 수 있다. I/O block은 입출력작업에서 발생하는 지연상태를 말한다. 사용자의 입력을 기다리는 경우를 예로 들수 있는데, 이런 경우 일시정지 상태에 있다가 사용자가 입력을 마치면 다시 실행대기 상태가 된다.
5. 지정된 일시정지시간이 다되거나(time-out), notify(), resume(), interrupt()가 호출되면 일시 정지상태를 벗어나 다시 실행대기열에 저장되어 자신의 차례를 기다리게 된다.
6. 실행을 모두 마치거나 stop()이 호출되면 쓰레드는 소멸된다.

> 실행을 위해 1부터 6까지 번호를 붙이기는 했지만 번호의 순서대로 쓰레드가 수행되는 것은 아니다.
> 

### static sleep(long millis)

- 실행중인 쓰레드 실행 지연
- sleep()에 의해 일시정지 상태가 된 쓰레드는 지정된 시간이 다 되거나 interrupt()가 호출되면, InterruptedException이 발생되어 잠에서 깨어나 실행대기 상태가 된다.
- sleep()을 호출 할때는 항상 try ~ catch 문으로 예외를 처리해줘야 한다.

```java
package day17;

class ThreadEx11_1 extends Thread {
	public void run() {
		for(int i = 0; i < 300; i++) {
			System.out.print("-");
		}
		System.out.print("<<th1 종료>>");
	}
}

class ThreadEx11_2 extends Thread {
	public void run() {
		for(int i = 0; i < 300; i++) {
			System.out.print("|");
		}
		System.out.print("<<th2 종료>>");
	}
}

public class ThreadEx11 {
	public static void main(String[] args) {
		ThreadEx11_1 th1 = new ThreadEx11_1();
		ThreadEx11_2 th2 = new ThreadEx11_2();
		th1.start();
		th2.start();
		
		try {
			th1.sleep(2000); 
		} catch(InterruptedException e) {}
		System.out.print("<<main 종료>>");
	}
}

실행결과
----------------------------------------|||------------------
||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||-------------
------------------------------------------------------------
--------------------------------||||---------------------
||||||||||||||||||||||||||||||||||-----------------------------------------
----||||--|||||||||||||||||------------------------------------------
---------------------|||||||||||||||||||||||||||||||||||||||||||||||||||||||||||------|||||
<<th1 종료>>||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||<<th2 종료>><<main 종료>>
```

- th1이 가장 먼저 종료 되었고, 그 다음이 th2, main의 순서인 것을 알수 있는데, th1.sleep(2000)으로 작성한 코드를 보았을대 th1이 가장 먼저 종료되었다는 것이 뜻밖이라고 생각할 수 있다.
- 그 이유는 sleep()은 항상 현재 실행 중인 쓰레드에 대해 작동하기 때문에 'th1.sleep(2000)'과 같이 호출하였어도 실제로 영향을 받는 것은 main메서드를 실행하는 main 메서드이다.
- sleep()은 static으로 선언되어 있으며, 참조변수를 이용해서 호출하기 보다는 'Thread.sleep(200);'과 같이 해야 한다.

> yield()가 static으로 선언되어 있는 것도 sleep()과 같은 이유이다.
> 

### interrupt()와 interrupted()

- interrupt() : interrupted 상태 값 변경 - true
InterruptedException 발생 →멈춰있는 쓰레드를 깨워주는 역활
- 단지 멈추라고 요청만 하는 것일 뿐 쓰레드를 강제 종료시키지는 못한다.
- interrupt()는 interrupted상태(인스턴스 변수)를 바꾸는 것일 뿐이다.
- interrupted()는 쓰레드에 대해 interrupt()가 호출되었는지 알려준다. interrupt()가 호출되지 않았다면 false를, interrupt()가 호출되었다면 true를 반환한다.
- boolean isInterrupted() :  interrupted 상태 값
(상태값만 조회)
- boolean interrupted() : interrupted 상태값
-> true -> false

```java
Thread th = new Thread();
th.start();
...
th.interrupt(); // 쓰레드 th에 interrupt()를 호출한다.

class MyThread extends Thread {
	public void run() {
		while(!interrupted()) { // interrupted()의 결과가 false인 동안 반복
			...
		}
	}
}

```

- interrupt()가 호출되면 interrupted()의 결과가 false에서 true로 바뀌어 while문을 벗어나게 된다.
- interrupted()와 달리 isInterrupted()는 쓰레드의 interrupted상태를 false로 초기화하지 않는다.

```java
void interrupt()   // 쓰레드의 interrupted 상태를 false에서 true로 변경.
boolean isInterrupted()  // 쓰레드의 interrupted 상태를 반환
static boolean interrupted()  // 현재 쓰레드의 interrupted상태를 반환 후, false로 변경

```

- 쓰레드가 sleep(), wait(), join()에 의해 '일시정지 상태(WAITING)'에 있을 때, 해당 쓰레드에 대해 interrupt()를 호출하면 sleep(), wait(), join()에서 InterruptedException이 발생하고 쓰레드는 '실행대기 상태(RUNNABLE)'로 바뀐다.(즉, 멈춰있던 쓰레드를 깨워서 실행가능한 상태로 만드는 것이다.)

day17/ThreadEx12.java

```java
package day17;

import javax.swing.JOptionPane;

class ThreadEx12_1 extends Thread {
	public void run() {
		int i = 10;

		while(i != 0 && !isInterrupted()) {
			System.out.println(i--);
			for(long x=0;x < 250000000000L;x++); // 시간 지연
		}
		System.out.println("카운트가 종료되었습니다.");
	}
}

public class ThreadEx12 {
	public static void main(String[] args) throws Exception {
		ThreadEx12_1 th1 = new ThreadEx12_1();
		th1.start();
		String input = JOptionPane.showInputDialog("아무 값이나 입력하세요.");
		System.out.println("입력하신 값은 " + input + "입니다.");
		th1.interrupt(); // interrupt()를 호출하면, interrupted상태가 true가 된다.
		System.out.println("isInterrupted():" +  th1.isInterrupted()); // true
	}
}

```

day17/ThreadEx13.java

```java
package day17;

import javax.swing.JOptionPane;

class ThreadEx13_1 extends Thread {
	public void run() {
		int i = 10;

		while(i != 0 && !isInterrupted()) {
			System.out.println(i--);
			try {
				Thread.sleep(1000); // 1초 지연
			} catch(InterruptedException e) {}
		}
		System.out.println("카운트가 종료되었습니다.");
	}
}

public class ThreadEx13 {
	public static void main(String[] args) throws Exception {
		ThreadEx13_1 th1 = new ThreadEx13_1();
		th1.start();
		String input = JOptionPane.showInputDialog("아무 값이나 입력하세요.");
		System.out.println("입력하신 값은 " + input + "입니다.");
		th1.interrupt(); // interrupt()를 호출하면, interrupted상태가 true가 된다.
		System.out.println("isInterrupted():" +  th1.isInterrupted()); // true
	}
}

실행결과
10
9
8
7
입력하신 값은 abcd입니다.
isInterrupted():false
6
5
4
3
2
1
카운트가 종료되었습니다.

```

- Thread.sleep(1000)으로 1초동안 지연되도록 변경하였다. 그러나 카운트가 종료되지 않았고 isInterrupted()의 결과가 false이다.
- Thread.sleep(1000)에서 InterruptedException이 발생했기 했기 때문이다.
- sleep()에 의해 쓰레드가 잠시 멈춰있을 때, interrupt()를 호출하면 InterruptedException이 발생되고 스레드의 interrupted상태는 false로 자동 초기화된다.
- 그럴때는 catch블럭에 interrupt()를 추가로 넣어줘서 쓰레드의 interrupted 상태를 true로 다시 바꿔줘여 한다.

변경 전

```java
try {
	Thread.sleep(1000);
} catch (InterruptedException e) {}

```

변경 후

```java
try {
	Thread.sleep(1000);
} catch (InterruptedException e) {
	interrupt();
}
```

### suspend() - 일시정지, resume() - 다시 시작, stop() - 중지
start() - 시작

- suspend(), resume(), stop()은 쓰레드의 실행을 제어하는 가장 손쉬운 방법이지만 suspend()와 stop()이 교착상태(deadlock)를 일으키기 쉽게 작성되어 있으므로 사용이 권장되지 않는다.
- suspend(), resume(), stop()의 문제를 해결하는 방법에 대한 예제

day17/ThreadEx14.java

```java
package day17;

public class ThreadEx14 {
	public static void main(String[] args) {
		ThreadEx14_1 th1 = new ThreadEx14_1("*");
		ThreadEx14_1 th2 = new ThreadEx14_1("**");
		ThreadEx14_1 th3 = new ThreadEx14_1("***");
		th1.start();
		th2.start();
		th3.start();
		
		try {
			Thread.sleep(2000);
			th1.suspend();
			Thread.sleep(2000);
			th2.suspend();
			Thread.sleep(3000);
			th1.resume();
			Thread.sleep(3000);
			th1.stop();
			th2.stop();
			Thread.sleep(2000);
			th3.stop();
		} catch (InterruptedException e) {}
	}
}

class ThreadEx14_1  implements Runnable {
	volatile boolean suspended = false;
	volatile boolean stopped = false;
	
	Thread th;
	
	ThreadEx14_1(String name) {
		th = new Thread(this, name);
	}
	
	public void run() {
		while(!stopped) {
			if (!suspended) {
				System.out.println(Thread.currentThread().getName());
				try {
					Thread.sleep(1000);
				} catch (InterruptedException e) {}
			}
		}
		System.out.println(Thread.currentThread().getName() + " - stopped");
	}
	
	public void suspend() {
		suspended = true;
	}
	
	public void resume() {
		suspended = false;
	}
	
	public void stop() {
		stopped = true;
	}
	
	public void start() {
		th.start();
	}
}

실행결과
*
***
**
*
***
**
***
*
**
***
**
***
***
***
*
***
*
***
*
***
** - stopped
* - stopped
***
***
*** - stopped
```

### yield()

- 다음쓰레드에게 작업 양보한다.
- 예를 들어 스케줄러에 의해 1초의 실행시간을 할당받은 쓰레드가 0.5초의 시간동안 작업한 상태에서 yield()가 호출되면, 나머지 0.5초는 포기하고 다시 실행대기상태가 된다.
- yield()와 interrupt()를 적절히 사용하면, 프로그램의 응답성을 높이고 보다 효율적인 실행이 가능하게 할 수 있다.

```java
package day17;

public class ThreadEx15 {
	public static void main(String[] args) {
		ThreadEx15_1 th1 = new ThreadEx15_1("*");
		ThreadEx15_1 th2 = new ThreadEx15_1("**");
		ThreadEx15_1 th3 = new ThreadEx15_1("***");
		th1.start();
		th2.start();
		th3.start();
		
		try {
			Thread.sleep(2000);
			th1.suspend();
			Thread.sleep(2000);
			th2.suspend();
			Thread.sleep(3000);
			th1.resume();
			Thread.sleep(3000);
			th1.stop();
			th2.stop();
			Thread.sleep(2000);
			th3.stop();
		} catch (InterruptedException e) {}
	}
}

class ThreadEx15_1  implements Runnable {
	volatile boolean suspended = false;
	volatile boolean stopped = false;
	
	Thread th;
	
	ThreadEx15_1(String name) {
		th = new Thread(this, name);
	}
	
	public void run() {
		String name = th.getName();
		
		while(!stopped) {
			if (!suspended) {
				System.out.println(Thread.currentThread().getName());
				try {
					Thread.sleep(1000);
				} catch (InterruptedException e) {
					System.out.println(name + " - interrupted");
				}
			} else { // 정지상태이면 다른 쓰레드로 바로 양보한다(넘긴다) - 응답성 향상 
				Thread.yield();
			}
		}
		System.out.println(Thread.currentThread().getName() + " - stopped");
	}
	
	public void suspend() {
		suspended = true;
		th.interrupt();
		System.out.println(th.getName() + " - interrupt() by suspend()");
		// interrupt()를 호출하면 sleep 구간을 건너띄고 바로 InterruptedException으로 건너띄므로 응답성이 좋아진다.
	}
	
	public void resume() {
		suspended = false;
	}
	
	public void stop() {
		stopped = true;
		th.interrupt();
		System.out.println(th.getName() + " - interrupt() by stop()");
		// interrupt()를 호출하면 sleep 구간을 건너띄고 바로 InterruptedException으로 건너띄므로 응답성이 좋아진다.
	}
	
	public void start() {
		th.start();
	}
}

실행결과
*
***
**
*
***
**
*
***
* - interrupted
* - interrupt() by suspend()
**
***
**
***
** - interrupted
** - interrupt() by suspend()
***
***
***
*
*
***
*
***
***
* - interrupted
* - stopped
* - interrupt() by stop()
** - interrupt() by stop()
** - stopped
***
*** - stopped
*** - interrupt() by stop()
```

### join()

- 다른 쓰레드의 작업을 기다렸다가 끝나면 실행

```java
void join()
void join(long millis)
void join(long millis, int nanos)

```

- 시간을 지정하지 않으면 해당 쓰레드가 작업을 모두 마칠 때까지 기다리게 된다. 작업 중에 다른 쓰레드의 작업이 먼저 수행되어야할 필요가 있을 때 join()을 사용한다.

```java
try {
	th1.join(); // 현재 실행중인 쓰레드가 쓰레드 th1의 작업이 끝날때까지 기다린다.
} catch (InterruptedException e) {}

```

- join()도 sleep()처럼 interrupt()에 의해 대기상태에서 벗어날 수 있으며, join()이 호출되는 부분을 try~catch문으로 감싸야 한다.
- join()은 sleep()과 유사한 점이 있지만 sleep()과 다른 점은 join()은 현재 쓰레드가 아닌 특정 쓰레드에 대해 동작하므로 static메서드가 아니라는 것이다.

> join()은 자신의 작업 중간에 다른 쓰레드의 작업을 참여(join)시킨다는 의미로 이름 지어진 것이다.
> 

day17/ThreadEx16.java

```java
package day17;

public class ThreadEx16 {
	static long startTime = 0;

	public static void main(String[] args) {
		ThreadEx16_1 th1 = new ThreadEx16_1();
		ThreadEx16_2 th2 = new ThreadEx16_2();
		th1.start();
		th2.start();
		startTime = System.currentTimeMillis();

		try {
			th1.join(); // main쓰레드가  th1의 작업이 끝날 때까지 기다린다.
			th2.join(); // main쓰레드가 th2의 작업이 끝날 때까지 기다린다.
		} catch (InterruptedException e) {}

		System.out.print("소요시간:" + (System.currentTimeMillis() - ThreadEx16.startTime));
	}
}

class ThreadEx16_1 extends Thread {
	public void run() {
		for(int i = 0; i < 300; i++) {
			System.out.print(new String("-"));
		}
	}
}

class ThreadEx16_2 extends Thread {
	public void run() {
		for(int i = 0; i < 300; i++) {
			System.out.print(new String("|"));
		}
	}
}

실행결과
---------|||||||||||||||||||||||||||||||||||||||||||||||||||||
||||||||||||||||||||||||||||||||||||||||||||----------|||||||
||||||||||||||||||||||||||||||||||||||||||--------|-------
--------------------------------------------
--------------||||||||||||||||||||||||||-------------
-----------------------------|||||||||||||||||||---
-----------------------------|||||||||||||||------
------------------------------------||||||||||||||
||||||||||||||||||||||--------------||||||||||----------
||||--|||||||||||||||-------------------------------
--------|||||||||||||||||||||||||||-------------|------
--------소요시간:19

```

- join()을 사용하지 않았으면 main쓰레드는 바로 종료된다.
- join()으로 쓰레드 th1, th2의 작업을 마칠 때 까지 main쓰레드가 기다리게 된다.

### 쓰레드의 동기화

- synchronized를 이용한 동기화

**메서드 전체를 임계영역으로 지정**

```java
public synchronized void calcSum() {
	...
}

```

- 메서드 전체가 임계 영역으로 설정된다. 쓰레드는 synchronized메서드가 호출된 시점부터 해당 메서드가 포함된 객체의 lock을 얻어 작업을 수행하다가 메서드가 종료되면 lock을 반환한다.

**특정한 영역을 임계 영역으로 지정**

```java
synchroninzed(객체의 참조변수) {
	...
}

```

- synchronized : 메서드 접근 제어자 뒤쪽

- sychronized블럭 영역 안으로 들어가면서 부터 쓰레드는 지정된 객체의 lock을 얻게 되고, 이 블럭을 벗어나면 lock을 반납한다.

- 상기 두 방법 모두 lock의 획득과 반납이 모두 자동적으로 이루어지므로 임계영역만 설정해 주면된다.
- 모든 객체는 lock을 하나씩 가지고 있으며 해당 lock을 가지고 있는 쓰레드만 임계 영역의 코드를 수행할 수 있다. 그리고 다른 쓰레드들은 lock을 얻을 때까지 기다리게 된다.
- 임계 영역은 멀티쓰레드 프로그램의 성능을 좌우하기 때문에 메서드 전체에 락을 거는 것 보다는 **sychronized블럭으로 임계영역을 최소화**하는 것이 좋다.

day17/Account.java

```java
package day17;

public class Account {
	private int balance = 1000;

	public int getBalance() {
		return balance;
	}

	public void withdraw(int money) {
		if (balance >= money) {
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {}
			balance -= money;
 		}
	}
}

```

day17/ThreadEx17.java

```java
package day17;

public class ThreadEx17 {
	public static void main(String[] args) {
		Runnable r = new RunnableEx17();
		new Thread(r).start();
		new Thread(r).start();
	}
}

class RunnableEx17 implements Runnable {
	Account acc = new Account();

	public void run() {
		while(acc.getBalance() > 0) {
			// 100, 200, 300중의 한 값으로 임의로 선택해서 출금(withdraw)
			int money = (int)(Math.random() * 3 + 1) * 100;
			acc.withdraw(money);
			System.out.println("balance:" + acc.getBalance());
		}
	}
}

실행결과
balance:600
balance:600
balance:400
balance:200
balance:200
balance:100
balance:-100
balance:-200

```

- 잔고가 0이상일 때(acc.getBalance() > 0) 출금이 가능하게 하는 조건이 있지만 잔고가 음수가 되었다.
- 그 이유는 한 쓰레드가 if문의 조건식을 통과하고 출금하기 바로 직전에 다른 쓰레드가 끼어들어서 출금을 먼저 했기 때문이다.
- 따라서 잔고를 확인하는 if문과 출금하는 문장은 하나의 임계 영역으로 묶여져야 한다.

동기화 예

```java
public synchronized void withdraw(int money) {
	if (balance >= money) {
		try {
			Thread.sleep(1000);
		} catch (InterruptedException e) {}
		balance -= money;
 	}
}

```

```java
public void withdraw(int money) {
	synchronized(this) {
		if (balance >= money) {
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {}
			balance -= money;
		}
	}
}

```

day17/Account2.java

```java
package day17;

public class Account2 {
	private int balance = 1000;

	public int getBalance() {
		return balance;
	}

	public synchronized void withdraw(int money) {
		if (balance >= money) {
			try {
				Thread.sleep(1000);
			} catch (InterruptedException e) {}
			balance -= money;
 		}
	}
}

```

day17/ThreadEx18.java

```java
package day17;

public class ThreadEx18 {
	public static void main(String[] args) {
		Runnable r = new RunnableEx18();
		new Thread(r).start();
		new Thread(r).start();
	}
}

class RunnableEx18 implements Runnable {
	Account2 acc = new Account2();
	
	public void run() {
		while(acc.getBalance() > 0) {
			// 100, 200, 300중의 한 값으로 임의로 선택해서 출금(withdraw)
			int money = (int)(Math.random() * 3 + 1) * 100;
			acc.withdraw(money);
			System.out.println("balance:" + acc.getBalance());
		}
	}
}

실행결과
balance:700
balance:600
balance:500
balance:200
balance:0
balance:0
```

### volatile

- CPU 코어의 캐시의 값을 사용 X, 직접 메모리(RAM)에서 접근
- 싱글코어 프로세서가 장착된 컴퓨터에서는 아무런 문제가 없으나 멀티코어 프로세서에서는 코어마다 별도의 캐시를 가지고 있기 때문에 변수값의 변경사항이 바로 반영이 되지 않을 수 있다.
- 코어는 메모리에서 읽어온 값을 캐지에 저장하고 캐시에서 값을 읽어서 작업한다. 다시 같은 값을 읽어올 때는 먼저 캐시에 있는지 확인하여 없을 때만 메모리에서 읽어온다.
- 그러다보니 도중에 메모리에 저장된 변수의 값이 변경이 되었는데도 캐시에 저장된 값이 갱신되지 않아서 메모리에 저장된 값이 다른 경우가 발생한다.
- 변수 앞에 **volatile**을 붙이면 코어가 변수의 값을 읽어올 때 캐시가 아닌 메모리에서 읽어오기 때문에 캐시와 메모리간의 불일치가 해결된다.

<img src="https://github.com/somi9954/Java/assets/137499604/01f0a8ac-de1d-4379-bcaa-e2366a396b3c" width="550">


```java
volatile boolean suspended = false;
volatile boolean stopped = false;
```
