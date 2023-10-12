## 가상 스레드의 도입 배경

**[ 기존 자바 스레드 모델의 문제와 한계 ]**</br>
자바 개발자들은 약 30년 동안 서버 애플리케이션의 동시성 처리를 위해 스레드를 사용해왔다. 대표적으로 스프링 프레임워크는 멀티 스레드 모델을 사용하고 있으며, 1개의 요청을 1개의 스레드가 처리하는 thread-per-request 방식으로 동작하고 있다. 따라서 동시 요청이 많다면 스레드의 수 역시 증가해야만 이에 대응할 수 있다.
하지만 기존 JDK의 스레드는 운영 체제(OS) 스레드의 Wrapper이기 때문에, 사용 가능한 스레드의 수가 하드웨어 수준보다 훨씬 적게 제한되어 있었다. OS 스레드는 비용이 높아 요청량에 비례하여 늘릴 수 없기 때문이다. 가질 수 있는 스레드의 양은 제한적인데, 자바 스레드는 OS 스레드의 Wrapper라서 I/O 작업을 만나면 블로킹되기까지 한다.
예를 들어 멀티 스레드 기반의 스프링 애플리케이션 서버에 요청이 들어왔다고 하자. 그러면 톰캣의 스레드 풀에 존재하는 스레드는 CPU를 가지고 요청을 처리하게 된다. 그러다가 네트워크 요청이나 파일 쓰기 같은 I/O 작업을 만나면 CPU를 OS에 반환하고 실행할 수 없는 상태(Non-Runnable)가 된다.
 , 자바 스레드는 OS 스레드의 Wrapper라서 I/O 작업을 만나면 블로킹되기까지 한다.
예를 들어 멀티 스레드 기반의 스프링 애플리케이션 서버에 요청이 들어왔다고 하자. 그러면 톰캣의 스레드 풀에 존재하는 스레드는 CPU를 가지고 요청을 처리하게 된다. 그러다가 네트워크 요청이나 파일 쓰기 같은 I/O 작업을 만나면 CPU를 OS에 반환하고 실행할 수 없는 상태(Non-Runnable)가 된다.
![image](https://github.com/somi9954/Java/assets/137499604/ca786476-c4bf-4c89-89d8-43bdf0c0c7aa)

Non-Runnable 상태에는 여러 가지 상태가 포함되는데, 이를 세분화하면 다음과 같다.
![image](https://github.com/somi9954/Java/assets/137499604/a8e40b9b-771e-482f-b56d-b58a89575083)

이로 인해 진행중인 스레드의 작업은 중단되고, I/O 작업이 끝날 때까지 대기한다. 그러다가 I/O 작업이 끝나면 남은 작업을 이어가고, 스레드를 스레드 풀에 반환한다.
만약 전체 스레드 3개 모두 네트워크 지연 등에 의해 블로킹된 상황에서 새로운 요청이 들어오면 어떻게 될까? 그러면 사용 가능한 스레드가 없으므로 새로운 요청은 톰캣의 내부 큐에서 대기하게 되고, 사용 가능한 스레드가 스레드 풀로 반환되면 그때서야 요청이 실행되고, 만약 요청이 지나치게 오래 대기하게 되면 에러가 반환된다.
![image](https://github.com/somi9954/Java/assets/137499604/cba5a28c-acfe-49e7-97e7-ddbea2a894e8)

오늘날에는 외부 API나 캐시 및 DB 등을 위해 수 많은 I/O 작업들이 필요한데, 해당 작업들마다 스레드가 잠들게 되니 비효율이 발생하는 것이다. 이를 위해 자바 개발자들은 이를 위해 여러 방안을 검토했다고 한다.
 
 
 
 
**[ 여러 가지 대안(Alternatives)에 대한 검토 ]** </br>
* 비동기 API에 계속 의존하기
* 코루틴(syntactic stackless coroutines)을 자바 언어에 추가하기
* user-mode 스레드를 나타내는 새로운 public class 추가하기
 
 
#### 비동기 API에 계속 의존하기
먼저 Future, CompletableFuture와 같은 비동기 API를 사용할 수 있다. 비동기 API는 반환 타입을 Future와 같은 특정 클래스로 감싸서 반환하는 방식을 사용한다.
```java
public void call() {
    CompletableFuture.supplyAsync(() -> 10)
        .thenCombine(CompletableFuture.supplyAsync(() -> 5), (r1, r2) -> (r1 + r2) * 2)
        .thenAccept(r -> System.out.println("Combined and Transformed Result: " + r))
        .exceptionally(ex -> {    
            System.err.println("An exception occurred: " + ex.getMessage());
            return null; // Return a default value or handle the exception as needed
    });
}
```
 
하지만 다음과 같은 이유로 비동기 API를 주된 해결책으로 삼지 않았다고 한다.
* 비동기 API는 동기식 코드와 결합되기 어려움
* 동일한 I/O 작업을 2가지로 표현하는 분리된 영역을 만듬
* 작업 순서에 대한 일관된 개념을 제공하지 않음
 
이것들 외에도 복잡한 여러 콤비네이터(thenCompose, thenAccept)을 학습해 적용해야 한다는 문제가 있다. 기술 스택이 바뀌면 새로운 콤비네이터를 학습해야 하는 부담도 있다. 따라서 비동기 API는 근본적인 해결법이 아니였다.
 
 
 
#### 코루틴(syntactic stackless coroutines)을 자바 언어에 추가하기
코루틴(coroutines)은 비동기 API 방식의 문제를 해결하기 위해 등장했다. 반환 결과를 감싸써 꾸미는 대신 새로운 제어자(modifer)로 마킹된 메소드를 비동기적으로 호출되도록 한다. 이는 기존의 동기식 코드에 “suspend” 같은 키워드만 추가하면 되므로 새롭게 학습할 필요가 없을 뿐만 아니라 예외 처리도 기존과 동일하게 try-catch로 할 수 있다. 대표적으로 자바스크립트는 async/await를, 코틀린은 suspend와 같은 키워드를 제공한다. 코루틴은 user-mode 스레드보다 구현하기 쉬우며 일련의 작업 컨텍스트를 나타내는 통합된 구조를 제공한다. 
```java
// suspend 제어자 추가
suspend fun postItem(Item item) {
    val token = requestToken();
    val post = createPost(token, item);
    processPost(post);
}
```
 
하지만 코루틴을 도입하게 되면 스레드용 API와 코루틴용 API로 자바 플랫폼이 나뉘게 되고, 자바 플랫폼의 모든 계층과 도구에 이러한 구조를 도입해야 한다. 자바 생태계는 이를 채택하는데 오래 걸릴 것이며, user-mode 스레드만큼 우아하게 플랫폼과 조화를 이루지 못할 것으로 판단했다. syntatic coroutines를 채택한 대부분의 언어는 각각의 제약으로 이를 선택했지만, 자바는 이러한 한계가 없었기에 굳이 문법적인 구문이 필요한 코루틴을 채택할 필요가 없었다.
* 코틀린: user-mode 스레드를 구현할 수 없음
* 자바스크립트: 단일 스레드에서 legacy semantic을 보장해야 함
* C++: 언어에 따른 기술적 제약이 존재함
 
 
#### 새로운 user-mode 스레드 클래스의 도입
자바 개발자들은 java.lang.Thread와 독립적인 새로운 user-mode 스레드의 도입을 고려했고, Thread 클래스를 통해 오랜 시간 쌓아온 부채를 버릴 좋은 기회라고 판단했다. 그래서 이 접근 방식의 여러 가지 변형을 찾고 프로토타입을 만들었지만, 모든 경우에 대해 기존 코드를 어떻게 실행할 것인지의 문제에 직면했다. 
가장 큰 문제는 Lock의 획득 여부 확인 또는 ThreadLocal 등을 위해 직/간접적으로 광범위하게 사용되고 있는 Thread.currentThread() 였다. 이 메소드는 현재 실행 중인 스레드를 나타내는 객체를 반환해야 한다. 만약 user-mode 스레드를 나타내는 새로운 클래스를 도입했다면, currentThread()는 일종의 래퍼 객체를 반환해야 할 것이다. 
현재 실행 중인 스레드를 나타내는 객체가 2개로 나뉘는 것은 혼란스러울 수 있으므로, 결국 기존 Thread API를 유지하는 것이 큰 문제는 아니라고 결론지었다. currentThread()와 같은 몇 가지 메서드를 제외하고는 개발자가 Thread API를 직접 사용하는 경우는 거의 없으며, 대부분 ExecutorService와 같은 고수준의 API를 사용하기 때문이다.
 
 
 
#### 그 외의 방안들
하드웨어를 최대한 활용하고자 하는 일부 개발자들은 스레드를 공유하는 방식을 사용하기도 한다. 대표적으로 리액티브 스택(Reactor) 기반의 스프링 웹플럭스(webflux)가 있다. 한 스레드가 I/O 작업이 끝나기를 기다리는(블로킹) 대신, 해당 스레드를 반납하여 다른 요청을 처리할 수 있도록 하는 것이다. I/O 작업은 제외하고 연산을 수행하는 동안에만 스레드를 보유하기 때문에 적은 수의 스레드로도 많은 동시 요청을 처리할 수 있다.
```java
public void call() {
      Flux.just(1, 2, 3, 4)
        .log()
        .map(i -> i * 2)
        .subscribe(elements::add);
  }
```
 
 
이를 통해 OS 스레드 부족으로 인한 처리량 제한을 없앴지만, 비용이 상당히 크다. 순차적인 것처럼 보이는 요청 처리 단계가 다른 스레드에서 실행될 수 있으며, 이로 인해 Stack Trace를 위한 컨텍스트를 제공할 수 없고, 요청 처리 로직을 순차적으로 살펴볼 수도 없다. 또한 러닝 커브가 상당히 높으며, 자바라는 프로그래밍 언어의 스타일과도 맞지 않는다.
 
 
 
**[ 기존 자바 스레드 모델의 문제와 한계 ]**</br>
따라서 자바 개발자들은 가상 스레드를 도입하게 되었고, 그 과정에서 다음을 핵심 목표로 삼았다.
* thread-per-request 스타일의 서버 애플리케이션이 하드웨어를 최적으로 활용할 수 있도록 한다.
* java.lang.Thread API를 사용하는 기존 코드가 최소한의 변경만으로 가상 스레드를 채택할 수 있도록 한다.
* 기존의 JDK 도구를 사용해 가상 스레드의 문제 해결, 디버깅 및 프로파일링을 쉽게 수행할 수 있도록 한다.
 
 
하드웨어를 최적으로 활용하지 못하는 근본적인 원인은 OS 스레드와 자바 스레드가 일대일 대응되기 때문이다. 즉, 자바 스레드가 실행되는 것은 OS 스레드가 사용중임을 의미한다. 따라서 해결 방안은 자바 런타임에서 OS 스레드와 일대일 대응되지 않는 더 효율적인 스레드를 구현해 사용하는 것이다. 운영 체제가 많은 가상 주소 공간을 제한된 양의 물리적 RAM에 매핑하여 메모리가 넉넉한 것처럼 보이게 하는 것처럼, 자바 런타임은 많은 수의 가상 스레드를 적은 수의 OS 스레드에 매핑하여 스레드가 넉넉한 것처럼 보이게 하는 것이다.
자바는 전체 실행 주기 동안 OS 스레드를 작아먹지 않는 java.lang.Thread 인스턴스를 도입하게 되었다. 즉, java.lang.Thread의 인스턴스로, OS 스레드와 연결되는 기존의 스레드인 플랫폼 스레드(Platform Thread)와 자바 런타임에만 존재하고 OS 스레드와는 연결되지 않는 신규 스레드인 가상 스레드(Virtual Thread)가 존재하게 되었다.

![image](https://github.com/somi9954/Java/assets/137499604/603088ab-d52b-4388-8adb-1b7340e9a94c)


 
 
가상 스레드는 OS가 아닌 JDK에서 제공하는 경량화된 user-mode 스레드이다. 특정 OS 스레드에 연결되지 않으므로 OS에서는 보이지 않으며, 존재를 인식하지 못한다.
가상 스레드는 CPU에서 연산을 수행하는 동안에만 OS 스레드를 사용한다. 만약 가상 스레드에서 실행 중인 코드가 I/O 작업을 호출하면, 자바 런타임은 논블로킹 OS 호출을 수행하고 가상 스레드를 자동으로 일시 중단한다. 이러한 방식은 논블로킹 스타일과 동일한 확장성을 제공하지만, 투명하게 달성된다는 점에서 차이가 있다.
자바 개발자에게 가상 스레드는 단지 생성 비용이 저렴하고 거의 무한대로 풍부한 스레드로, 대부분은 수명이 짧고 호출 스택이 얕으며, 단일 HTTP 호출 또는 단일 JDBC 쿼리 정도만 수행한다. 이를 통해 하드웨어 활용도가 최적에 가까워져 높은 수준의 동시성을 구현하고 결과적으로 높은 처리량을 제공하며, 기존의 자바 플랫폼 및 도구들과 조화를 이룬다.
 
 
 
 
## 2. 가상 스레드의 도입 배경

**[ 기존 자바 API의 변화 ]**</br>
대표적으로 기존의 자바 API에 다음과 같은 변화가 있었으며, 이것들 외에도 Debugging 관련 도구, JFR(JDK Fligh Rcorder), JMX(Java Management Extensions) 등에도 추가적인 변화가 있었다.
 
 
#### java.lang.Thread
Thread.Builder, Thread.ofVirtual(), Thread.ofPlatform()는 새로운 스레드를 생성하는 신규 API이다. Thread.Builder를 사용하면 단일 Thread 뿐만 아니라 동일한 속성의 여러 스레드를 갖는 ThreadFactory도 생성할 수 있다. 아래는 시작되지 않은 mangkyu라는 이름의 새로운 가상 스레드를 생성하고 실행하는 코드이다.
```java
Thread thread = Thread.ofPlatform()
    .name("mangkyu")
    .unstarted(runnable);

Thread thread = Thread.ofVirtual()
    .name("mangkyu")
    .unstarted(runnable);

Thread.startVirtualThread(Runnable);
 ```
 
현재 스레드가 가상 스레드인지 검사하려면 다음의 메소드를 사용할 수 있다.
```java
boolean isVirtual = Thread.isVirtual();
```
 
Thread.getAllStackTraces()를 호출하면 전체 플랫폼 스레드의 스택 트레이스를 맵으로 제공해준다.
```java
Map<Thread, StackTraceElement[]> map = Thread.getAllStackTraces();
```
 
Thread API에서 플랫폼 스레드와 가상 스레드의 차이를 정리하면 다음과 같다.
* Thread 클래스의 퍼블릭 생성자로는 가상 스레드를 만들 수 없다.
* 가상 스레드는 항상 데몬 스레드이며 Thread.setDaemon(boolean)으로도 비데몬 스레드로 바꿀 수 없다.
* 가상 스레드의 우선 순위는 Thread.NORM_PRIORITY로 고정되어 있으며 Thread.setPriority(int)으로도 바꿀 수 없다.
* 가상 스레드는 스레드 그룹의 active member가 아니다. 가상 스레드에서 Thread.getThreadGroup()를 호출하면 “VirtualThreds”라는 이름의 placeholder 스레드 그룹을 반환한다. Thread.Builder API는 가상 스레드의 스레드 그룹을 설정하는 메소드를 갖고 있지 않다.
* 가상 스레드는 SecurityManager 집합과 실행될 권한이 없다.
 
 
#### Thread-local(스레드 로컬)
가상 스레드는 플랫폼 스레드와 마찬가지로 ThreadLocal과 InheritableThreadLocal을 지원한다. 그러나 가상 스레드는 매우 많을 수 있으므로, 신중히 고려하여 사용해야 한다. 특히 스레드 풀의 한 스레드가 여러 작업을 위해 비싼 리소스를 풀링하는 경우에 스레드 로컬을 사용하지 않아야 한다. 따라서 JDK의 기본 모듈에서도 가상 스레드를 위해 스레드 로컬을 사용하는 코드들을 많이 제거함으로써 수백만 개의 스레드가 실행될 때 메모리 공간을 줄였다.
jdk.traceVirtualThreadLocals 시스템 속성을 true로 설정하면 가상 스레드가 ThreadLocal에 값을 설정할 때의 stack trace를 얻을 수 있다. 이는 가상 스레드를 사용하도록 코드를 마이그레이션 할 때 도움이 된다. 이후에 추가될 Scoped value는 스레드 로컬의 더 좋은 대안이 될 수 있다.
 
 
#### java.util.concurrent
잠금을 위한 기본 API인 java.util.concurrent.LockSupport도 가상 스레드를 지원한다. 가상 스레드가 파킹되면 플랫폼 스레드는 다른 작업을 수행할 수 있도록 해제되고, 가상 스레드가 파킹해제되면 작업이 계속 진행되도록 플랫폼 스레드를 스케줄링한다. LockSupport의 변경으로 이를 사용하는 모든 API(Locks, Semaphores, Blocking Queues 등)가 가상 스레드에서 호출될 때 정상적으로 파킹할 수 있다.
또한 Executors.newThreadPerTaskExecutor(ThreadFactory) 및 Executors.newVirtualThreadPerTaskExecutor()는 각 작업에 대해 새 스레드를 생성하는 ExecutorService를 생성한다. 이를 통해 Thread Pool과 ExecutorService를 사용하는 기존 코드의 마이그레이션과 상호 운용이 가능하다.
 
 
#### Networking
java.net와 java.nio.channels 패키지의 네트워킹 API도 가상 스레드를 지원한다. 네트워크 연결을 설정하거나 소켓에서 읽는 등 가상 스레드에서 블로킹 작업을 수행하면, 플랫폼 스레드가 다른 작업을 수행할 수 있도록 해제시킨다.
InterruptibleChannel에서 획득한 소켓에서 수행하는 블로킹 I/O 연산은 항상 중단 가능했기 때문에, 이 변경으로 인해 생성자로 생성될 때와 채널에서 가져올 때의 동작이 일치하게 된다.
 
 
#### java.io
java.io 패키지는 바이트와 문자 스트림에 대한 API를 제공한다. 해당 API 구현은 synchronized에 상당히 의존하며, 가상 스레드가 고정되지 않도록 변경이 필요하다.
 
 
#### JNI(Java Native Interface)
JNI는 객체가 가상 스레드인지 테스트하는 새로운 함수 IsVirtualThread를 제공한다.
 
 
 
 
**[ 가상 스레드를 통한 처리량 향상 ]** </br>
아래는 10000개의 가상 스레드를 생성하는 예제 코드이다. 이때 JDK는 10000개의 가상 스레드를 위해 적은 수의 OS 스레드(아마도 하나)를 사용할 것이다. 만약 이 코드가 10000개의 플랫폼 스레드를 생성한다면, 10000개의 OS 스레드를 생성하려고 시도할 것이고, 장비와 운영체제에 따라 문제가 생길 수 있다.
```java
try (var executor = Executors.newVirtualThreadPerTaskExecutor()) {
    IntStream.range(0, 10_000).forEach(i -> {
        executor.submit(() -> {
            Thread.sleep(Duration.ofSeconds(1));
            return i;
        });
    });
}  // executor.close() is called implicitly, and waits
```
 
스레드 풀을 통해 약 200개 정도의 플랫폼 스레드를 재사용하더라도, 결국 초당 200개 씩만 처리할 수 있기 때문에 크게 개선되지 않는다. 반면에 가상 스레드는 충분한 워밍헙 후에 초당 약 10000개를 처리할 수 있다.

![image](https://github.com/somi9954/Java/assets/137499604/1ae1ce7c-87af-43a0-b40f-065ac0e92369)


 
 
만약 중간의 sleep 없이 계산만 수행한다면, 가상 스레드든 플랫폼 스레드든 프로세서 코어 수를 초과하여 스레드를 늘리는 것은 도움이 되지 않는다. 가상 스레드는 더 빠른 스레드가 아니므로, 플랫폼 스레드보다 코드를 더 빠르게 실행하지는 않는다. 가상 스레드는 속도(시간 단축)이 아닌 확장성(높은 처리량)을 제공하기 위해 존재한다.
따라서 가상 스레드는 다음의 경우에 애플리케이션 처리량을 크게 향상시킬 수 있다.
* 동시 작업 수가 많고(수천 개 이상)
* 작업이 CPU에 종속되지 않는 경우(I/O 작업)</br>
 
 
가상 스레드가 일반적인 서버 애플리케이션의 처리량 개선에 도움되는 이유는 하나의 작업이 대기(waiting)에 많은 시간을 소비하는 여러 I/O 작업(API 호출, 캐시, DB 등)들을 포함하기 때문이다. 만약 CPU에 종속적인 작업들(json 변환, 연산 등)만 존재한다면 성능이 개선되지 않는다. 왜냐하면 프로세서 코어가 실질적으로 스레드를 가지고 일을 하는데, 코어가 놀지 않고 계속해서 일을 한다면 스레드가 많다고 하더라도 코어가 부족하여 처리량이 향상될 수 없기 때문이다. 성능 향상은 I/O 작업에 의해 스레드가 블로킹될 때, 놀고 있는 코어를 활용해야 가능하다.
![image](https://github.com/somi9954/Java/assets/137499604/71e3953c-7d12-4ae6-84e5-7b173311353e)



 
 
 
 
## 3. 가상 스레드 참고 및 주의 사항

**[ 가상 스레드 풀링 금지 ]**</br>
풀링은 고가의 리소스를 공유하기 위한 것이다. 하지만 가상 스레드는 라이프사이클 동안 하나의 작업만 실행하도록 설계되었으므로 절대 풀링해서는 안된다. 따라서 풀링 없이 항상 새롭게 생성해주면 된다. 만약 애플리케이션 코드에서 스레드 풀 기반의 ExecutorService를 사용중이라면 가상 스레드 기반의 ExecutorService로 마이그레이션 해야 한다.
```java
var executor = Executors.newFixedThreadPool(10)
var executor = Executors.newVirtualThreadPerTaskExecutor()
```
 
동시 요청의 수를 제한하기 위해 스레드 풀(Thread Pool)을 사용하는 코드도 풀링 대신 세마포어 등을 사용하도록 수정해야 한다. 또한 개발자는 스레드 로컬을 사용해 한 스레드의 작업 간에 값비싼 리소스를 공유하기도 한다. 이때도 모든 가상 스레드 별로 값비싼 리소스를 생성하면 성능이 크게 저하될 수 있으므로 이를 사용하지 않고 값비싼 리소스를 매우 많은 가상 스레드에서 효율적으로 공유할 수 있는 캐싱 전략을 사용하도록 수정해야 한다.
 
 
 
**[ java.io를 상속받는 기존 코드에서 주의할 점 ]**</br>
java.io.BufferedInputStream, BufferedOutputStream, BufferedReader, BufferedWriter, PrintStream, PrintWriter에서 사용되는 내부 잠금 프로토콜(문서에 작성되지 않음)의 변경은 I/O 메소드가 synchronized 된다고 가정하는 코드에 영향을 줄 수 있다. 이는 해당 클래스들을 상속받아 부모클래스에 의해 잠금을 가정하는 코드나 java.io.Reader 또는 java.io.Writer를 확장하고 해당 API에 의해 접근 가능한 Lock 객체를 사용하는 코드에는 영향을 주지 않는다.
 
 
 
**[ 가상 스레드 모니터링을 위한 스레드 덤프 ]**</br>
실행 중인 프로그램의 상태를 명확히 제공하는 것은 문제 해결, 시스템 운영 및 관리, 최적화를 위해 필수적이다. JDK는 오랫동안 스레드를 디버그, 프로파일링 및 모니터링하는 메커니즘을 제공해왔다. 대표적으로 스레드 덤프는 thread-per-request 기반의 애플리케이션 문제 해결을 위해 널리 사용되어 왔다. 가상 스레드도 결국 java.lang.Thread의 인스턴스이므로 많은 작업이 필요함에도 동일한 기능을 제공해야 한다.
jstack 또는 jcmd로 얻는 JDK의 기존 스레드 덤프는 수평적인 스레드 목록을 제공한다. 이는 적은 수의 플랫폼 스레드에는 적합하지만 수 많은 가상 스레드에는 적합하지 않다. 따라서 기존 스레드 덤프를 확장하지 않고, 플랫폼 스레드와 함께 가상 스레드를 의미 있는 방식으로 그룹화하여 표시하는 새로운 종류의 스레드 덤프를 jcmd에 도입하였다.
```java
jcmd <pid> Thread.dump_to_file -format=json <file>
```
 
새로운 스레드 덤프는 기존의 정보들 중 일부(object addresses, locks, JNI statistics, heap statistics 등)를 제공하지 않는다. 또한 많은 스레드를 나열해야 할 수 있으므로 스레드 덤프를 생성 시에 애플리케이션이 일시 중지되지 않는다.
jdk.trackAllThreads 시스템 프로퍼티를 false로 설정되면 Thread.Builder API로 직접 생성된 가상 스레드는 런타임에 추적되지 않으며 새로운 스레드 덤프에도 등장하지 않을 것이다. 대신 네트워크 I/O 작업에 블록된 가상 스레드와 new-thread-per-task ExecutorService로 생성된 가상 스레드들만 보일 것이다. 아래는 새롭게 생성된 스레드 덤프의 예시이다.

![image](https://github.com/somi9954/Java/assets/137499604/4acb0996-661d-4770-8970-fc9851e6b8a1)


 
 
 
**[ 가상 스레드의 실행과 스케줄링 ]**</br>
어떤 작업을 수행하려면 프로세서 코어에 스레드를 할당해야 하는데, 가상 스레드가 JDK 자체 스케줄러에 의해 플랫폼 스레드에 마운트되면, 플랫폼 스레드가 OS 스케줄러에 의해 프로세서 코어에 할당되어 작업이 수행된다. JDK의 스케줄러는 FIFO로 동작하는 work-stealing ForkJoinPool으로, LIFO로 동작하는 ParallelStream 풀과 독립적이다. 
스케줄러를 통해 가상 스레드를 할당하는 플랫폼 스레드를 virtual thread’s carieer라고 한다. 기본적으로 스케줄러의 병렬성은 캐리어의 수(프로세서의 수)와 같지만  jdk.virtualThreadScheduler.parallelism 시스템 속성으로 조정할 수 있다.
캐리어는 가상 스레드와 플랫폼 스레드의 관계를 유지하지 않으므로, 가상 스레드는 라이프사이클 동안 다른 플랫폼 스레드에 마운트될 수 있다. 예를 들어 가상 스레드는 1번 플랫폼 스레드에서 일부 코드를 실행한 후 마운트 해제되고, 자유로워진 1번 플랫폼 스레드는 스케줄러를 통해 다른 가상 스레드를 마운트한다. 그러면 기존의 가상 스레드는 다른 플랫폼 스레드에 다시 마운트될 수 있다.
![image](https://github.com/somi9954/Java/assets/137499604/c01db38a-b975-46b4-b6af-272641df540b)


일반적으로 가상 스레드는 I/O나 JDK의 블로킹 연산(예를 들어 BlockingQueue.take() 등)에 의해 블로킹될 때 마운트 해제(unmount)된다. 블로킹 연산이 완료되면 다시 가상 스레드를 스케줄러에 제출해 마운트하여 실행을 재개한다. 참고로 가상 스레드의 마운트/언마운트는 OS 스레드를 차단하지 않으며, 빈번하고 투명하게 발생한다.
예를 들어 다음과 같이 블로킹 연산이 있는 코드가 있다고 하자. 일반적으로 get()을 호출할 때마다 한 번씩, send()에서 I/O를 수행하는 과정에서 가상 스레드의 마운트/언마운트가 여러 번 반복될 수 있다. 대부분의 블로킹 작업은 가상 스레드를 언마운트하여 캐리어와 OS 스레드가 새로운 작업을 수행할 수 있도록 하지만, 사용자 코드는 가상 스레드가 플랫폼 스레드에 할당되는 방법이나 시기를 가정해서는 안된다.
```java
response.send(future1.get() + future2.get());
``` 
 
블로킹 작업에서 가상 스레드가 캐리어에 고정되어 언마운트 할 수 없는 상황도 있다.
* synchronized 블록이나 메소드에서 코드를 실행할 때(향후 릴리스에서 제거 가능)
* 네이티브 메소드 또는 외부 함수를 실행할 때
 
 
가상 스레드가 캐리어에 고정된다고 해서 애플리케이션에 문제가 있는 것은 아니지만 확장성을 저해할 수 있다. 가상 스레드가 고정되는 동안 I/O 또는 BlockingQueue.take()와 같은 블로킹 작업을 수행하면, 캐리어와 OS 스레드가 같이 블로킹되기 때문이다.
이때 스케줄러는 가상 스레드 고정을 보완하기 위해 병렬성을 확장하지는 않는다. 대신, 자주 실행되고 잠재적으로 긴 I/O 작업을 보호하는 synchronized 블록이나 메소드를 수정해 빈번하고 오래 지속되는 고정을 피하고, java.util.concurrent.locks.ReentrantLock을 사용하도록 한다. 드물게 사용되거나(시작 시에만 사용되는 경우 등) 인메모리 연산을 보호하는 synchronized 블록이나 메소드는 변경할 필요가 없다.
자바는 이러한 부분을 진단할 수 있는 도구를 제공한다. 이를 통해 가상 스레드로 마이그레이션하고 synchronized로 작성된 부분을 java.util.concurrent의 lock으로 대체해야 하는지 평가하는데 도움을 줄 것이다.
* JDK Fligh Recorder(JFR) 이벤트는 가상 스레드가 고정된다면 발행될 것이다.
* jdk.tracePinnedThreads 시스템 속성은 스레드가 고정된 상태에서 블로킹되면 스택 트레이스를 출력한다.
 
 
tracePinnedThreads=full로 실행하면 전체 스택 트레이스를 출력하고, 기존 프레임과 고정된 프레임을 강조 표시한다. tracePinnedThreads=short로 실행하면 문제있는 프레임만 출력된다.
일부 블로킹 작업은 OS나 JDK의 제한(대규모 파일 시스템 작업 또는 Object.wait() 등) 때문에 캐리어와 OS 스레드를 모두 블로킹하여, 스케줄러의 병렬성을 일시적으로 확장는 방식으로 OS 스레드 점유를 보완하기도 한다. 이때 스케줄러의 ForkJoinPool에 있는 플랫폼 스레드 수가 일시적으로 사용 가능한 프로세서 수를 초과할 수 있는데, jdk.virtualThreadScheduler.maxPoolSize 시스템 속성으로 최대값을 조정할 수 있다.
 
 
 
 
## 4. 자바의 가상 스레드(Virtual Thread) 요약

**[ 자바의 가상 스레드(Virtual Thread) 요약 ]**
* 기존 자바의 스레드는 OS 스레드와 일대일 대응되도록 구현됨
* 이로 인해 스레드의 개수가 제한되며, I/O 작업 시에 블로킹되어 하드웨어를 최적으로 활용하지 못함
* 다른 언어들은 제약으로 인해 비동기 API, 코루틴 등으로 문제를 해결했지만 자바는 제약이 없음
* JVM 수준에서 이를 처리하고 기존 코드와의 호환성을 유지하는 방식으로 문제를 해결함
* 가상 스레드는 비용이 저렴한 스레드이므로 풀링하지 말아야 함
* 또한 수백만 개의 가상 스레드가 리소스를 공유할 수 있으므로 ThreadLocal은 주의해서 사용해야 함
 
 
 
자바 진영(스프링 MVC)에서는 멀티 스레드 모델을 동시성 처리 방법으로 사용해왔고, 이로 인해 I/O 요청이 들어오면 스레드가 블로킹되면서 자원이 낭비되곤 했다. 코틀린과 같은 언어에서 코루틴을 이용해 이를 해결했지만, 이를 위해 특정 키워드(async-await 또는 suspend 등과 같은)를 통해 논블로킹 구간을 지정해주어야 했다. 자바에는 코루틴을 도입한 다른 언어들과 달리 기술적 제약이 없었기에, 특정 키워드 없이 기존 코드와 호환되는 방식으로 가상 스레드를 제공할 수 있었다. 덕분에 가상 스레드를 도입한다고 하여 새로운 개념을 배우거나 프로그램을 재작성할 필요가 없다. 물론 오늘날의 높은 스레드 비용에 대처하기 위한 습관들은 버려야 할 수 있다.
 
 
-----
https://mangkyu.tistory.com/309의 자료를 인용하였습니다
 
참고 자료
https://openjdk.org/jeps/444
https://www.infoq.com/news/2023/09/java-21-so-far
https://wiki.openjdk.org/display/loom
https://www.techtarget.com/searchsoftwarequality/news/365533479/Java-20-Project-Loom-updates-set-stage-for-Java-LTS
http://guruma.github.io/posts/2018-09-27-Project-Loom-Fiber-And-Continuation/
http://guruma.github.io/posts/2018-11-18-Continuation-Concept/
