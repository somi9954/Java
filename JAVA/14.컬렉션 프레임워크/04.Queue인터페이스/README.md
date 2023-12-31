# Queue인터페이스

- 처음에 저장한 데이터를 가장 먼저 쓰게 되는 FIFO(First In First Out)구조로 되어 있다.
- 데이터를 꺼낼때 항상 첫번째 저장된 데이터를 삭제하므로 데이터의 추가/삭제가 쉬운 LinkedList로 구현하는것이 적합하다.
- Queue는 최근사용문서, 인쇄작업 대기기록, 버퍼(buffer)와 같은곳에서 활용이 된다.
- Queue을 선언하는 방법은 다음과 같다

```java
Queue<Integer> q = new LinkedList<>();
```

![image](https://github.com/somi9954/Java/assets/137499604/91db0dd6-4ff7-4409-80ef-389591e91e47)

- Queue 클래스와 추가 된 메서드는 다음과 같다

| 메서드 | 설명 |
| --- | --- |
| boolean add(Object o) | 지정된 객체를 큐에 저장한다. 성공하면 true 반환한다. 저장공간이 부족하면 IIIegalStateException 발생한다. |
| Object remove() | 큐에서 객체를 꺼내 반환한다. 비어있으면 NoSuchElementException 발생한다. |
| Object element() | 삭제없이 요소 읽어온다(스택의 peek과 달리 Queue가 비었을때 NoSuchElementException이 발생된다.) |
| boolean offer(Object o) | 큐에 객체 저장한다. 성공하면 true, 실패시 false 반환한다. |
| Object poll() | 큐에서 객체를 꺼내서 반환한다. 비어있으면 null반환한다 |
| Object peek() | 삭제없이 요소 읽어온다. Queue가 비어있으면 null을 반환한다. |


```java
import java.util.LinkedList;
import java.util.ListIterator;
import java.util.Queue;
import java.util.Scanner;

public class Queue {
    static Queue q = new LinkedList();
    static final int MAX_SIZE = 5;	// Queue에 최대 5개까지만 저장되도록 한다.

    public static void main(String[] args) {
        System.out.println("help를 입력하면 도움말을 볼 수 있습니다.");

        while(true) {
            System.out.print(">>");
            try {
                // 화면으로부터 라인단위로 입력받는다.
                Scanner s = new Scanner(System.in);
                String input = s.nextLine().trim();

                if("".equals(input)) continue;

                if(input.equalsIgnoreCase("q")) {
                    System.exit(0);
                } else if(input.equalsIgnoreCase("help")) {
                    System.out.println(" help - 도움말을 보여줍니다.");
                    System.out.println(" q 또는 Q - 프로그램을 종료합니다.");
                    System.out.println(" history - 최근에 입력한 명령어를 "
                            + MAX_SIZE +"개 보여줍니다.");
                } else if(input.equalsIgnoreCase("history")) {
                    int i=0;
                    // 입력받은 명령어를 저장하고,
                    save(input);

                    // LinkedList의 내용을 보여준다.
                    LinkedList tmp = (LinkedList)q;
                    ListIterator it = tmp.listIterator();

                    while(it.hasNext())
                        System.out.println(++i+"."+it.next());
                } else {
                    save(input);
                    System.out.println(input);
                } // if(input.equalsIgnoreCase("q")) {
            } catch(Exception e) {
                System.out.println("입력오류입니다.");
            }
        } // while(true)
    } //  main()
    public static void save(String input) {
        // queue에 저장한다.
        if(!"".equals(input))
            q.offer(input);

        // queue의 최대크기를 넘으면 제일 처음 입력된 것을 삭제한다.
        if(q.size() > MAX_SIZE)  // size()는 Collection인터페이스에 정의
            q.remove();
    }
} // end of class
```

<img src="https://github.com/somi9954/Java/assets/137499604/eb9f2618-a81b-4492-b07e-b58183e07b1d" width="360">


## ****PriorityQueue 클래스****

- 먼저 들어온 순서대로 데이터가 나가는 것이 아닌 우선 순위를 먼저 결정하고 우선순위가 높은 엘리먼트가 먼저 나가는 구조이다.(큐에 들어가는 원소는 비교가 가능한 기준이 있어야 한다.)
- 우선순위 큐(Priority Queue)는 힙을 이용하여 구현하는게 일반적이다.
- 데이터를 삽입할 때 우선순위를 기준으로 최대힙 혹은 최소 힙을 구성하고 데이터를 꺼낼 때 루트 노드를 얻어낸 뒤 루트 노드를 삭제할 때는 빈 루트 노드 위치에 맨 마지막 노드를 삽입한 후 아래로 내려가면서 적절한 자리를 찾아서 옮기는 방식으로 진행됩니다.
- 내부 요소는 힙으로 구성되어 이진트리 구조로 이루어져 있다.
- Priority Queue 선언하는 방법은 다음과 같다.

```java
import java.util.PriorityQueue; //import

//int형 priorityQueue 선언 (우선순위가 낮은 숫자 순)
PriorityQueue<Integer> priorityQueue = new PriorityQueue<>();

//int형 priorityQueue 선언 (우선순위가 높은 숫자 순)
PriorityQueue<Integer> priorityQueue = new PriorityQueue<>(Collections.reverseOrder());

//String형 priorityQueue 선언 (우선순위가 낮은 숫자 순)
PriorityQueue<String> priorityQueue = new PriorityQueue<>(); 

//String형 priorityQueue 선언 (우선순위가 높은 숫자 순)
PriorityQueue<String> priorityQueue = new PriorityQueue<>(Collections.reverseOrder());
```

만약 높은 숫자가 우선순위가 되게 하고 싶다면 선언 시 Collections.reverseOrder() 메서드를 활용합니다.

### **Priority Queue 값 추가**

```java
priorityQueue.add(1);     // priorityQueue 값 1 추가
priorityQueue.add(2);     // priorityQueue 값 2 추가
priorityQueue.offer(3);   // priorityQueue 값 3 추가
```

자바의 우선순위 큐에 값을 추가하고 싶다면 add(value) 또는 offer(value)라는 메서드를 활용하면 됩니다. add(value) 메서드의 경우 만약 삽입에 성공하면 true를 반환하고, 큐에 여유 공간이 없어 삽입에 실패하면 IllegalStateException을 발생시킵니다. 우선순위 큐에 값을 추가한다면 아래 그림과 같은 과정을 통해 즉시 정렬이 됩니다.

<img src="https://github.com/somi9954/Java/assets/137499604/a2f16d88-d122-4e45-9589-9c8051f4c11d" width="360">

### **Priority Queue 값 삭제**

```java
priorityQueue.poll();       // priorityQueue에 첫번째 값을 반환하고 제거 비어있다면 null
priorityQueue.remove();     // priorityQueue에 첫번째 값 제거
priorityQueue.clear();      // priorityQueue에 초기화
```

우선순위 큐에서 값을 제거하고 싶다면 poll()이나 remove()라는 메서드를 사용하면 됩니다. 값을 제거할 시 우선순위가 가장 높은 값이 제거됩니다. poll() 함수는 우선순위 큐가 비어있으면 null을 반환합니다. pop을 하면 가장 앞쪽에 있는 원소의 값이 아래 그림과 같이 제거됩니다. queue의 모든 요소를 제거하려면 clear() 메서드를 사용합니다.

<img src="https://github.com/somi9954/Java/assets/137499604/712d2a24-8a33-42bb-b565-8c0bc0176cdb" width="360">


### **Priority Queue에서 우선순위가 가장 높은 값 출력**

```java
PriorityQueue<Integer> priorityQueue = new PriorityQueue<>();//int형 priorityQueue 선언
priorityQueue.offer(2);     // priorityQueue에 값 2 추가
priorityQueue.offer(1);     // priorityQueue에 값 1 추가
priorityQueue.offer(3);     // priorityQueue에 값 3 추가
priorityQueue.peek();       // priorityQueue에 첫번째 값 참조 = 1
```

Priority Queue에서 우선순위가 가장 높은 값을 참조하고 싶다면 peek()라는 메서드를 사용하면 됩니다. 위의 예시에서는 우선순위가 가장 높은 1이 출력됩니다.

```java
// 우선순위 큐에 저장할 객체는 필수적으로 Comparable를 구현
class Student implements Comparable<Student> {
    String name; // 학생 이름
    int priority; // 우선순위 값

    public Student(String name, int priority) {
        this.name = name;
        this.priority = priority;
    }

    @Override
    public int compareTo(Student user) {
        // Student의 priority 필드값을 비교하여 우선순위를 결정하여 정렬
        if (this.priority < user.priority) {
            return -1;
        } else if (this.priority == user.priority) {
            return 0;
        } else {
            return 1;
        }
    }

    @Override
    public String toString() {
        return "Student{" +
                "name='" + name + '\'' +
                ", priority=" + priority +
                '}';
    }
public static void main(String[] args) {

    // 오름차순 우선순위 큐
    Queue<Student> priorityQueue = new PriorityQueue<>();

    priorityQueue.add(new Student("주몽", 5));
    priorityQueue.add(new Student("세종", 9));
    priorityQueue.add(new Student("홍길동", 1));
    priorityQueue.add(new Student("임꺽정", 2));

    // 우선순위 대로 정렬되어 있음
    System.out.println(priorityQueue);
    // [Student{name='홍길동', priority=1}, Student{name='임꺽정', priority=2}, Student{name='주몽', priority=5}, Student{name='세종', priority=9}]

    // 우선순위가 가장 높은 값을 참조
    System.out.println(priorityQueue.peek()); // Student{name='홍길동', priority=1}

    // 차례대로 꺼내기
    System.out.println(priorityQueue.poll()); // Student{name='홍길동', priority=1}
    System.out.println(priorityQueue.poll()); // Student{name='임꺽정', priority=2}
    System.out.println(priorityQueue.poll()); // Student{name='주몽', priority=5}
    System.out.println(priorityQueue.poll()); // Student{name='세종', priority=9}
}
}
```

![image](https://github.com/somi9954/Java/assets/137499604/3907f319-4eed-478d-8beb-77d43a904a0e)


## Deque 인터페이스

![image](https://github.com/somi9954/Java/assets/137499604/d8861d7e-b87b-4017-ad0e-781a93bd8bcc)


- Deque(Double-Ended Queue)는 양쪽으로 넣고 빼는 것이 가능한 큐를 말한다
- 스택과 큐를 하나로 합쳐놓은 것과 같으며 스택으로 사용할 수도 있고, 큐로 사용할 수도 있다.
- Deque의 조상은 Queue이며, 구현체로 ArrayDeque와 LinkedList 등이 있다.
- 선언하는 방법은 다음과 같다.

```java
Deque<Integer> deque = new LinkedList<>();
Integer형 선언
```

![image](https://github.com/somi9954/Java/assets/137499604/fd646dc3-8e30-4ecc-ad64-d7b41e88ab41)


**addFirst()**

덱의 앞쪽에 엘리먼트를 삽입한다. 용량 제한이 있는 덱의 경우, 용량을 초과하면 예외(Exception)가 발생한다

**offerFirst()**

덱의 앞쪽에 엘리먼트를 삽입한다. 정상적으로 엘리먼트가 삽입된 경우 true가 리턴되며, 용량 제한에 걸리는 경우 false를 리턴한다.

**addLast()**

덱의 마지막 쪽에 엘리먼트를 삽입한다. 용량 제한이 있는 덱의 경우, 용량 초과시 예외가 발생한다

**add()**

addLast()와 동일

**offerLast()**

덱의 마지막 쪽에 엘리먼트를 삽입한다. 정상적으로 엘리먼트가 삽입된 경우 true가 리턴되며, 용량 제한에 걸리는 경우 false를 리턴한다.

![image](https://github.com/somi9954/Java/assets/137499604/6900b157-7cb5-4fcb-8e96-59c17aa905d8)

**removeFirst()**

덱의 앞쪽에서 엘리먼트 하나를 뽑아서 제거한 다음 해당 엘리먼트를 리턴한다. 덱이 비어있으면 예외가 발생한다.

**pollFirst()**

덱의 앞쪽에서 엘리먼트 하나를 뽑아서 제거한 다음 해당 엘리먼트를 리턴한다. 덱이 비어있으면 null 이 리턴된다.

**removeLast()**

덱의 마지막 쪽에서 엘리먼트 하나를 뽑아서 제거한 다음 해당 엘리먼트를 리턴한다. 덱이 비어있으면 예외가 발생한다.

**pollLast()**

덱의 마지막 쪽에서 엘리먼트 하나를 뽑아서 제거한 다음 해당 엘리먼트를 리턴한다. 덱이 비어있으면 null 이 리턴된다.

**remove()**

removeFirst()와 동일

**poll()**

pollFirst()와 동일

![image](https://github.com/somi9954/Java/assets/137499604/db1eabba-ce22-4bbd-9c59-fe8b1a459fcb)

**getFirst()**

덱의 앞쪽 엘리먼트 하나를 제거하지 않은채 리턴한다. 덱이 비어있으면 예외가 발생한다

**peekFirst()**

덱의 앞쪽 엘리먼트 하나를 제거하지 않은채 리턴한다. 덱이 비어있으면 null이 리턴된다.

**getLast()**

덱의 마지막쪽 엘리먼트 하나를 제거하지 않은채 리턴한다. 덱이 비어있으면 예외가 발생한다.

**peekLast()**

덱의 마지막 엘리먼트 하나를 제거하지 않은 채 리턴한다. 덱이 비어있으면 null이 리턴된다.

**peek()**

peekFirst()와 동일

**removeFirstOccurrence(Object o)**

덱의 앞쪽에서부터 탐색하여 입력한 Object o와 동일한 첫 엘리먼트를 제거한다. Object o 와 같은 엘리먼트가 없으면 덱에 변경이 발생하지 않는다.

**removeLastOccurrence(Object o)**

덱의 뒤쪽에서부터 탐색하여 입력한 Object o와 동일한 첫 엘리먼트를 제거한다. Object o 와 같은 엘리먼트가 없으면 덱에 변경이 발생하지 않는다.

**element()**

removeFirst()와 동일

**addAll(Collection <? extends E c)**

입력 받은 Collection의 모든 데이터를 덱의 뒤쪽에 삽입한다.

**push()**

addFirst()와 동일. 덱을 스택으로 사용할 때 쓰임

**pop()**

removeFirst()와 동일. 덱을 스택으로 사용할 때 쓰임

**remove(Object o)**

removeFirstOccurrence(Object o)와 동일

**contain(Object o)**

덱에 Object o와 동일한 엘리먼트가 포함되어 있는지 확인

**size()**

덱의 크기

**iterator()**

덱의 앞쪽부터 순차적으로 실행되는 이터레이터(iterator)를 얻어옴

**descendingIterator()**

덱의 뒤쪽부터 순차적으로 실행되는 이터레이터(iterator)를 얻어옴

```java
public static void main(String[] args) throws InterruptedException {
      
        System.out.println("Stack!!");
        Deque<String> stack = new ArrayDeque<>();
        stack.addFirst("Element1");
        stack.addFirst("Element2");
        stack.addFirst("Element3");
        System.out.println(stack.removeFirst());
        System.out.println(stack.removeFirst());
        System.out.println(stack.removeFirst());
      
        System.out.println("Queue!!");
        Deque<String> queue = new ArrayDeque<>();
        queue.addFirst("Element1");
        queue.addFirst("Element2");
        queue.addFirst("Element3");
        System.out.println(queue.removeLast());
        System.out.println(queue.removeLast());
        System.out.println(queue.removeLast());
    }
```

<img src="https://github.com/somi9954/Java/assets/137499604/1b1cff9b-0a68-4cf4-a4ea-108d3479f6b7" width="360">

## ****LinkedList 클래스****

- LinkedList는 List 인터페이스와 Queue 인터페이스를 동시에 상속받고 있기 때문에, 스택 / 큐 로서도 응용이 가능하다.
- 자료들을 반드시 연속적으로 배열시키지는 않고 임의의 공간에 기억시키되, 자료 항목의 순서에 따라 노드의 포인터 부분을 이용하여 서로 연결시킨 구조이다.
- 실제로 LinkedList 클래스에 큐 동작과 관련된 메서드를 지원한다. (push, pop, poll, peek, offer ..등)

<img src="https://github.com/somi9954/Java/assets/137499604/d9949fac-1413-4575-8d95-44892afcee00" width="360">


💡 큐(queue)는 데이터를 꺼낼 때 항상 첫 번째 저장된 데이터를 삭제하므로, ArrayList와 같은 배열 기반의 컬렉션 클래스를 사용한다면, 데이터를 꺼낼 때마다 빈 공간을 채우기 위해 데이터의 이동 & 복사가 발생하므로 비효율적이다. 그래서 큐는 ArrayList보다 데이터의 추가/삭제가 용이한 LinkedList로 구현하는 것이 적합하다.


- LinkedList 구현하기

```java
package exam02;

public class MyListNode {
            //리스트 객체

        private String data; // 데이터
        public MyListNode next; // 다음 노드를 가리키는 링크

        public MyListNode() {
            //디폴트 생성자

            //맴버 변수 null 로 초기화
            data = null;
            next = null;
        }

        public MyListNode(String data) {

            //data를 매개변수로 갖는 생성자
            this.data = data;

            this.next = null;
        }

        public MyListNode(String data, MyListNode link) {
            // date 와 다음 요소를 가리키는 MyListNode 형의 link 로 초기화
            this.data = data;
            this.next = link;
        }

        public String getData() {
            return data; //데이터 반환
        }
    }
```

```java
package exam02;

public class MyLinkedList {
    private MyListNode head; //첫번째 노드
    int count; //데이터 수

    public MyLinkedList() {

        //생성자
        //맴버 변수 초기화
        head = null;
        count = 0;
    }

    public MyListNode addElement( String data ) {

        MyListNode newNode;

        if(head == null) {

            newNode = new MyListNode(data); //다음 노드가 없기 때문에, data 매개변수로 생성
            head = newNode; //첫번째 노드로 현재 노드 설정
        }
        else {

            newNode = new MyListNode(data); //마지막 노드이기 때문에 다음노드가 없으므로, data 매개변수로 생성
            MyListNode temp = head; //현재 맨 첫 노드를 ..임시로 담을 변수에 설정
            while(temp.next != null) {
                //처음부터 끝까지 : 마지막 노드를 찾아서 [ 자신의 다음 노드가 없는 노드 ]
                temp = temp.next;
            }
            temp.next = newNode; //마지막 노드에 추가할 노드 넣기
        }
        count++; //노드 수 증가

        return newNode; //새로 삽입한 노드 반환
    }

    public MyListNode insertElement(int position, String data) {

        int i;
        MyListNode tempNode = head;
        MyListNode newNode = new MyListNode(data);

        if(position < 0 || position > count) {
            System.out.println("추가 할 위치 오류. 현재 리스트 개수 : " + count );
            return null;
        }

        if(position == 0) {
            //맨 앞으로 들어가는 경우
            newNode.next = head; //새로 들어갈 노드의 다음 노드는 현재 맨 앞에 있는 노드로 설정
            head = newNode; //맨 앞노드는 새로 들어갈 노드로 설정
        }else {
            //맨 앞으로 들어가는 경우가 아닌 경우
            MyListNode preNode = null; //앞 노드를 담을 변수
            for(i=0; i<position; i++) {
                preNode = tempNode; // 넣을 위치의 이전 노드를 설정
                tempNode = tempNode.next; //임시노드에 다음 노드를 설정
            }
            newNode.next = preNode.next; //새로운 노드의 다음 노드는 이전노드의 다음노드로 설정
            preNode.next = newNode; //이전노드의 다음 노드는 새로운노드로 설정

        }
        count++; //노드 수 증가

        return newNode; //삽입된 노드 반환
    }

    public MyListNode removeElement(int position) {

        int i ;
        MyListNode tempNode = head;

        if(position >= count ){
            System.out.println("삭제 할 위치 오류입니다. 현재 리스트의 개수는 " + count +"개 입니다.");
            return null;
        }

        if(position == 0){  //맨 앞을 삭제하는
            head = tempNode.next;
        }
        else {
            MyListNode preNode = null;
            for(i=0;i<position; i++) {
                preNode = tempNode;         //삭제할 위치의 이전노드
                tempNode = tempNode.next;	//삭제할 노드 설정
            }
            preNode.next = tempNode.next; //이전 노드의 다음 노드는 삭제할 노드의 다음 노드로 설정
        }
        count--; //노드 수 1감소
        System.out.println(position + "번째 항목이 삭제되었습니다.");

        return tempNode; //삭제한 노드 반환
    }

    public String getElement(int position)
    {
        // 노드의 데이터 반환 메소드
        int i;
        MyListNode tempNode = head;

        if(position >= count ){
            //검색할 위치가 노드 수보다 크거나 같은 경우
            System.out.println("검색 위치 오류 입니다. 현재 리스트의 개수는 " + count +"개 입니다.");
            return new String("error");
        }

        if(position == 0){  //맨 첫번째 노드인 경우

            return head.getData();
        }

        for(i=0; i<position; i++){
            //처음부터 찾는 노드 위치의 까지 탐색
            tempNode = tempNode.next;

        }
        // 찾는 노드 데이터 반환
        return tempNode.getData();
    }

    public MyListNode getNode(int position)
    {
        //찾는 노드 반환 메소드
        int i;
        MyListNode tempNode = head;

        if(position >= count ){
            System.out.println("검색 위치 오류 입니다. 현재 리스트의 개수는 " + count +"개 입니다.");
            return null;
        }

        if(position == 0){  //맨 첫 노드인경우

            return head;
        }

        for(i=0; i<position; i++){
            tempNode = tempNode.next;

        }
        return tempNode; //찾는 노드 반환
    }

    public void removeAll()
    {
        //노드 전체 삭제
        head = null;
        count = 0;

    }

    public int getSize()
    {
        //사이즈 반환
        return count;
    }

    public void printAll()
    {
        //전체 출력

        if(count == 0){
            System.out.println("출력할 내용이 없습니다.");
            return;
        }

        //첫 노드 부터 마지막 노드까지 출력
        MyListNode temp = head;

        while(temp != null){
            System.out.print(temp.getData());
            temp = temp.next;
            if(temp!=null){
                System.out.print("->");
            }
        }
        System.out.println("");
    }

    public boolean isEmpty()
    {
        //비었는지 체크
        if(head == null) return true;
        else return false;
    }
}
```

```java
package exam02;

public interface IQueue {
        //IQueue 인터페이스

        public void enQueue(String data); //데이터 삽입

        public String deQueue(); //데이터 삭제

        public void printAll(); //전체 요소 출력
    }
```

```java
package exam02;

public class MyListQueue extends MyLinkedList implements IQueue {

    //연결리스트를 상속받고, IQueue 인터페이스 구현

    MyListNode front;
    MyListNode rear;

    public MyListQueue() {
        // TODO Auto-generated constructor stub

        // 큐 초기화
        front = null; // 큐의 맨 앞 연결리스트
        rear = null; // 큐의 맨 뒤 연결리스트
    }

    @Override
    public void enQueue(String data) {
        // TODO Auto-generated method stub

        // 큐에 데이터 삽입

        // 새로운 연결리스트 노드 데이터 정의
        MyListNode newNode;
        if (isEmpty()) {

            //큐가 비어있다면

            //새 데이터 삽입 후
            newNode = addElement(data);

            // 큐의 front의 rear 모두 새로운 노드로 초기화
            front = newNode;
            rear = newNode;
        } else {

            //큐가 비어있지 않다면

            //새 데이터 삽입 후
            newNode = addElement(data);
            // rear를 새로운 노드로 지정 [맨 뒤]
            rear = newNode;
        }
        System.out.println(newNode.getData() + " added");

    }

    @Override
    public String deQueue() {
        // TODO Auto-generated method stub

        if (isEmpty()) {

            //큐가 비어있다면 삭제할 데이터 없음
            System.out.println("Queue is Empty");
            return null;
        }

        //맨 앞 데이터부터 삭제 [가장 먼저 들어온 데이터]
        String data = front.getData();
        //맨 앞 데이터로 front 노드의 다음노드로 front 설정
        front = front.next;
        if (front == null) {
            //맨 앞 노드가 null이면 맨 뒤 노드도 null로 설정
            rear = null;
        }

        //삭제할 데이터 반환
        return data;
    }

    public void printAll() {
        //큐의 모든 데이터 출력
        if (isEmpty()) {
            System.out.println("Queue is Empty");
            return;
        }

        //임시 노드에 현재 큐의 맨 앞 노드 대입
        MyListNode temp = front;
        while (temp != null) {
            System.out.print(temp.getData() + ",");
            //맨 앞노드의 다음노드로 대입
            temp = temp.next;
        }
        System.out.println();
    }
}
```

```java
package exam02;

public class MyListQueueTest {
    public static void main(String[] args) {
        // TODO Auto-generated method stub
        MyListQueue listQueue = new MyListQueue();
        listQueue.enQueue("A");
        listQueue.enQueue("B");
        listQueue.enQueue("C");
        listQueue.enQueue("D");
        listQueue.enQueue("E");

        System.out.println(listQueue.deQueue());
        listQueue.printAll();

    }
}
```

<img src="https://github.com/somi9954/Java/assets/137499604/0a27e802-aec7-4180-ba46-2b6bb4ad6604" width="360">

## ****ArrayDeque 클래스****

- 스택으로 사용할 때 Stack 클래스보다 빠르며, 대기열로 사용할 때는  LinkedList보다 빠르다.
- 사이즈에 제한이 없다. 하지만 멀티 쓰레드가 지원이 되지 못한다.
- null 요소는 저장이 되지 않는다.

```java
Deque<Integer> deque = new ArrayDeque<>();

deque.offerLast(100); // [100]
deque.offerFirst(10); // [10, 100]
deque.offerFirst(20); // [20, 10, 100]
deque.offerLast(30); // [20, 10, 100, 30]

deque.pollFirst(); // 20 <- [10, 100, 30]
deque.pollLast(); // [10, 100] -> 30
deque.pollFirst(); // 10 <- [100]
deque.pollLast(); // [] -> 100
```
