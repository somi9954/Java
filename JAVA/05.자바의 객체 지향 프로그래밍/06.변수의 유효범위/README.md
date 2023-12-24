## 변수의 유효범위

1. 지역변수
    - 함수가 호출되었을때 스택에서 공간을 할당 받고, 실행이 끝나면 제거되는 변수
    - 함수 지역에서만 유효한 변수
2. 멤버변수(인스턴스 변수)
    - 객체 생성시 힙에서 공간을 할당 받고, 참조가 끊기면 가비지 콜렉터(GC) 제거
3. static 변수
    - 클래스 로더 -> 데이터 영역에서 생성, 애플리케이션이 종료 될때 제거
    

static 응용 - 싱글톤 패턴
- 하나의 필요할때만 생성해서 객체를 공유

참고)
공유하는 변수, 메서드
- 기능과 관련된 클래스를 가지고 객체를 많이 생성하는 경우가 적다
- 기능과 관련된 클래스 -> 메서드를 static으로만 정의 하는경우가 있다.
예) java.lang.Math

- static으로만 정의하면 처음부터 활성화, 메모리 공간을 차지 : 사용하지 않아도 불필요한 메모리가 소비
- 회원 가입

만드는 방법
1) 생성자의 접근 제어자를 private : 외부에서 생성 불가
2) 객체를 클래스 내부에서 생성
3) 외부에서 생성된 객체를 접근할 수 있는 메서드 정의

### 싱글톤 패턴

싱글톤 패턴이란 **클래스의 인스턴스를 하나만 생성하여 사용하는 패턴이다.**

주로 특정 객체를 여러곳에서 **공유**해야 할 때 사용한다.(Ex: DB Conntection pool)

싱글톤 패턴을 이용함으로써 최초에 한번만 메모리를 할당하고(static) 그 메모리 인스턴스 하나를 등록해 여러 쓰레드에서 동시에 하나의 객체를 이용할 수 있게 할 수 있다.

이것으로 인해 주의할 점은 **여러곳에서 동시에 접근해서 생길 수 있는 문제(동기화 문제)**를 잘 파악하고 설계해야한다.

싱글톤 패턴을 만들땐 기본적으로 **생성자를 private로 해서 외부에서는 직접 인스턴스를 생성할 수 없게 하고**, 사용자에게 인스턴스를 전달하는 **static 메소드**가 있다. 아래 예제를 보자.

아래 예제를 보면 객체는 오로지 **getInstance()를 통해서만 생성되거나 얻을 수 있다.** 이로인해 예제 출력을 해도 1이 두번 출력된다.

```java
public class Singleton {
    //싱글톤 객체를 static 변수로 선언
    private static Singleton instance;
    private int msg;
    
    //외부에서 생성자 호출 막기
    private Singleton(int msg) {
        this.msg = msg;
    }

    //인스턴스를 전달
    public static Singleton getInstance(int msg) {
        if (instance == null) {
            instance = new Singleton(msg);
        }
        return instance;
    }

    public void printMsg() {
        System.out.println(msg);
    }
}

class Main {
    public static void main(String[] args) {
        Singleton instance = Singleton.getInstance(1);
        Singleton instance2 = Singleton.getInstance(2);
        instance.printMsg();
        instance2.printMsg();
    }
}

결과
1
1
```

하지만 위의 코드의 경우 문제점이 있다.

> 문제점
> 

아래 예제를 보자. 아래 예제를 실행하면 쓰레드를 통해 동시에 Singleton객체에 접근해 여러개의 객체가 생성되는 것을 볼 수 있다. 왜냐하면 **모든 쓰레드가 거의 동시에 도착하고 이로인해 서로가 null 객체를 바라보기 때문에 쓰레드들이 객체를 생성한다**. 이것을 **동시성 문제**라 한다.

```java
public class Singleton {
    private static Singleton instance;
    private int msg;

    private Singleton(int msg) {
        try {
            Thread.sleep(100);
            this.msg = msg;
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    public static Singleton getInstance(int msg) {
        if(instance == null) {
            instance = new Singleton(msg);
        }
        return instance;
    }

    public int getMsg() {
        return msg;
    }
}

class Main {
    public static int num = 1;
    public static void main(String[] args) {
        Runnable run = () -> {
            num++;
            Singleton singleton = Singleton.getInstance(num);
            System.out.println("instance : " + singleton.getMsg());
        };
        for (int i = 0; i < 10; i++) {
            Thread thread = new Thread(run);
            thread.start();
        }
    }
}
//실행마다 달라짐
결과
instance : 6
instance : 5
instance : 4
instance : 8
instance : 2
instance : 11
instance : 3
instance : 7
instance : 9
instance : 10
```

이러한 동시성 문제(Thread Safe)를 해결하기 위한 방법을 살펴보자.

### 2. 다양한 싱글톤 구현 방법

> Eager initailization(이른 초기화, Thread safe)
> 

이 구현 방법은 클래스의 static 특징을 이용해 **클래스 로더가 초기화하는 시점에 인스턴스를 메모리에 등록하는 방법이다**. 아래처럼 static **변수 선언과 동시에 초기화**를 해주면 동시성 문제를 해결할 수 있다.

```java
publicclassSingleton {
    //선언과 동시에 초기화
privatestatic Singleton instance =new Singleton(0);
privateint msg;

privateSingleton(int msg) {
try {
            Thread.sleep(100);
this.msg = msg;
        }catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
publicstatic SingletongetInstance() {
return instance;
    }
publicintgetMsg() {
return msg;
    }
}
classMain {
publicstaticint num = 1;
publicstaticvoidmain(String[] args) {
        Runnable run = () -> {
            num++;
            Singleton singleton = Singleton.getInstance();
            System.out.println("instance : " + singleton.getMsg());
        };
for (int i = 0; i < 10; i++) {
            Thread thread =new Thread(run);
            thread.start();
        }
    }
}
결과
instance : 0
instance : 0
instance : 0
instance : 0
instance : 0
instance : 0
instance : 0
instance : 0
instance : 0
instance : 0
```

> Lazy Initialization with synchronized(게으른 초기화, 동기화 블럭)
> 

이 방법은 **synchronized** 키워드를 이용한 방식이다

synchronized는 기본적으로 동기화를 보장해주는 키워드로 **일반 메소드에 synchronized를 선언하면 그 실행된 메소드의 인스턴스는 하나의 쓰레드만 접근**할 수 있다. 즉, synchronized가 선언된 메소드의 인스턴스가 2개가 있다면 **각 인스턴스마다 하나의 쓰레드가 접근**할 수 있다.

하지만 static에 synchronized를 선언하면 **클래스의 클래스 객체를 기준으로 동기화가 이루어진다**. JVM에는 클래스당 하나의 클래스가 객체가 적재된다. 즉, static synchronized는 같은 **클래스 객체당 하나의 쓰레드만 접근**할 수 있다.

그래서 아래의 예제의 경우 하나의 쓰레드만 접근할 수 있으므로 동시성 문제를 해결 할 수 있다.

하지만 synchronized의 문제점은 성능이 좋지 않다는 것이다. 즉, 인스턴스를 많이 가져오는 작업을 할 경우 성능이슈가 발생할 수 있다.

```java
publicclassSingleton {
privatestatic Singleton instance;
privateint msg;

privateSingleton(int msg) {
try {
            Thread.sleep(100);
this.msg = msg;
        }catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
    //synchronized 키워드 사용
publicstaticsynchronized SingletongetInstance(int msg) {
if(instance ==null) {
            instance =new Singleton(msg);
        }
return instance;
    }

publicintgetMsg() {
return msg;
    }
}

classMain {
publicstaticint num = 1;
publicstaticvoidmain(String[] args) {
        Runnable run = () -> {
            num++;
            Singleton singleton = Singleton.getInstance(num);
            System.out.println("instance : " + singleton.getMsg());
        };
for (int i = 0; i < 10; i++) {
            Thread thread =new Thread(run);
            thread.start();
        }
    }
}
결과
instance : 2
instance : 2
instance : 2
instance : 2
instance : 2
instance : 2
instance : 2
instance : 2
instance : 2
instance : 2
```

> Lazy Initialization. Double Checking Locking(DCL)
> 

Double Checking Locking은 위에서 본 synchronized 키워드를 사용한 방법의 단점을 보완한 방법이다.

위에서 말했다시피 synchronized는 메소드를 호출하는 것은 많은 비용이 든다. 그래서 아래 처럼 sychronized 블럭을 null일 경우에만 접근하게하여 성능저하를 보완할 수 있다.

```java
publicclassSingleton {
privatestatic Singleton instance;
privateint msg;

privateSingleton(int msg) {
try {
            Thread.sleep(100);
this.msg = msg;
        }catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

publicstatic SingletongetInstance(int msg) {
if (instance ==null) {
            //instance가 null인 경우 synchronized 블록 접근
synchronized (Singleton.class) {
if (instance ==null) {
                    instance =new Singleton(msg);
                }
            }
        }
return instance;
    }

publicintgetMsg() {
return msg;
    }
}
classMain {
publicstaticint num = 1;

publicstaticvoidmain(String[] args) {
        Runnable run = () -> {
            num++;
            Singleton singleton = Singleton.getInstance(num);
            System.out.println("instance : " + singleton.getMsg());
        };
for (int i = 0; i < 10; i++) {
            Thread thread =new Thread(run);
            thread.start();
        }
    }
}
```

> Lazy Initialization. LazyHolder
> 

이 방법은 클래스안에 클래스를 두는 holder방법을 이용한 것이다.아래 코드에서 중첩 클래스의 instance는 getInstance()가 호출되기 전까지는 초기화 되지않는다. 또한 instance는 static이므로 클래스 로딩 시점에 한번만 호출되고 final을 사용해 다시 값이 할당되지 않도록 함으로써 동시성 문제를 해결할 수 있다.

가장 성능이 좋고 많이 쓰이는 방식이다.

```java
publicclassSingleton {
privatestatic Singleton instance =new Singleton(0);
privateint msg;

privateSingleton(int msg) {
try {
            Thread.sleep(100);
this.msg = msg;
        }catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
    //static 클래스안에 static 멤버 변수 선언 및 초기화
privatestaticclassInitial {
privatestaticfinal Singleton instance =new Singleton(0);
    }
publicstatic SingletongetInstance() {
return Initial.instance;
    }

publicintgetMsg() {
return msg;
    }
}

classMain {
publicstaticint num = 1;
publicstaticvoidmain(String[] args) {
        Runnable run = () -> {
            num++;
            Singleton singleton = Singleton.getInstance();
            System.out.println("instance : " + singleton.getMsg());
        };
for (int i = 0; i < 10; i++) {
            Thread thread =new Thread(run);
            thread.start();
        }
    }
}
```
