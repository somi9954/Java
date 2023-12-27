# List인터페이스(순차자료구조)

- 배열과 유사한 자료 구조로 중복이 허용되면서 저장 순서가 유지되는 구조를 제공한다.
- List 인터페이스를 생성하여 기능을 정의하고 하위 클래스에 상속해 그 기능을 구현하도록 한다.
- 대표적으로 List 인터페이스를 상속하여 구현한 ArrayList, LinkendList, Vector 등을 List 계열 자료 구조로 사용한다.
- 배열과 달리 크기가 가변적이므로 데이터의 추가, 삭제 등이 용이하다.

<img src="https://github.com/somi9954/Java/assets/137499604/a8cc5e1f-9915-4ed3-84ce-2cc39b68e050" width="350">

## List인터페이스에 정의된 메서드

Collection 인터페이스로부터 상속받은 것은 제외하였다.

| 메서드 | 설명 |
| --- | --- |
| void add(int index, Object element)boolean addAll(int index, Collection c) | 지정된 위치(index)에 객체(element) 또는 컬렉션에 포함된 객체들을 추가한다. |
| Object get(int index) | 지정된 위치(index)에 있는 객체를 반환한다. |
| int indexOf(Object o) | 지정된 객체의 위치(index)를 반환한다.(List의 첫 번째 요소로부터 순방향으로 찾는다.) |
| int lastIndexOf(Object o) | 지정된 객체의 위치(index)를 반환한다.(List의 마지막 요소로 부터 역방향으로 찾는다.) |
| ListIterator listIterator()ListIterator listIterator(int index) | List의 객체에 접근할 수 있는 ListIterator를 반환한다. |
| Object remove(int index) | 지정된 위치(index)에 있는 객체를 삭제하고 삭제된 객체를 반환한다. |
| Object set(int index, Object element) | 지정된 위치(index)에 객체(element)를 저장한다. |
| void sort(Comparator c) | 지정된 비교자(Comparator)로 List를 정렬한다. |
| List subList(int fromIndex, int toIndex) | 지정된 범위(fromIndex부터 toIndex)에 있는 객체를 반환한다. |

### ArrayList

- 가장 많이 사용하는 List 인터페이스의 대표적인 구현 클래스이다.
- JDK1.2부터 제공된 ArrayList는 내부적으로 **배열을 이용**해 구현되어 배열과의 호환성이 좋은 구조 자료이다.
- 조회 속도는 빠르다.
- 배열은 크기를 변경할 수 없고 만약 크기를 늘리고자 한다면 새로운 배열을 만들어서 기존의 값들을 옮겨야 하는 과정을 거쳐야 합니다.
- 요소의 추가 및 삭제 작업에 걸리는 시간이 매우 길어지는 단점을 가지게 됩니다. → 매번 새로운 배열이 생성 ⇒ 성능 저하 문제
- 스택의 구현체를 만들기 적합한 구조
- 선언하는 방법은 다음과 같다.

```java
List < 데이터 타입 > list = new ArrayList<데이터타입> ();
		       제네릭               선언객체    제네릭
```

- 지정되는 데이터는 항상 객체형으로 지정해야 한다. int형, long형, double형과 같은 기본 자료형은 대응하는 Wrapper 클래스를 이용하여 지정한다

<aside>
💡 List<E> list = new ArrayList<>();
JDK 1.7이후부터는 Collection의 선언이 간소화 되었다.

</aside>

- ArrayList **데이터 저장**

: add(E e), 또는 add(int index, E e)메서드를 사용한다. E는 리스트 선언시 지정한 객체를 의미한다.

add(E e)를 사용하게 되면 마지막 데이터  뒤에 차례대로 삽입이 된다.  삽입 시에는 index가 부여되며 배열과 마찬가지로 순차적으로 부여된다.

<img src="https://github.com/somi9954/Java/assets/137499604/7b8409a5-aa3e-4681-8221-349de4578d78" width="350">

 add(int index, E e) 메서드는 원하는 index 위치에 데이터를 삽입할 수 있다. 그러나 연속성 없이 순서를 부여해 삽입하는건 불가능하다. 

예를 들어 3개가 들어 있는 데이터의 List가 있을 시에 해당 리스트에서 index가 1인, 즉 2번째 위치에 데이터를 삽입할 경우 아래와 같이 진행된다.

<img src="https://github.com/somi9954/Java/assets/137499604/5f1c4032-2e92-4b40-b101-40d2ad7f864f" width="350">


그림과 같이 데이터 삽입을 원하는 위치에 기존 데이터가 존재한다면 기존 데이터는 뒤로 이동하게 되고 새로운 데이터가 그 자리에 추가 된다. 하지만 추가를 원하는 위치가 연속성이 없는 위치라면 문법적으로는 오류가 발생하지 않지만 실행시 오류가 발생한다.

<img src="https://github.com/somi9954/Java/assets/137499604/4b1a82bb-7f6d-45b9-96f7-583adafe3de9" width="350">

- ArrayList **데이터 치환**

: List 에 저장된 데이터를 변경할 수 있다. 변경을 원하는 Index 위치와 치환할 값 또는 객체를 지정하면 해당 위치의 값이 변경 된다. 이때 사용하는 메서드는 다음과 같다.

```java
void set(int index, E value);
```

- ArrayList **데이터 삭제**

: List의 데이터 삭제는 단지 데이터만 삭제되는 것이 아니라  해당 위치 공간까지 삭제 된다. 배열의 경우 공간이 생성되면 삭제는 할 수 없지만, List는 원하는 위치의 공간을  삭제할 수 있으며 빈 공백을 메우기 위해 데이터들이 앞으로 이동한다.

<img src="https://github.com/somi9954/Java/assets/137499604/bca43341-1524-4994-8925-908d70d4d2f3" width="350">

데이터를 삭제할 때는 remove()메서드를 이용한다. 해당 메서드는 remove(int index), remove(Object o) 두가지가 있는데, remove(int index)는 index를 이용해 특정 위치의 데이터를 삭제하고, remove(Object o)는 저장한 데이터를 삭제한다. 

전체가 삭제를 하려면 뒤에서 부터 삭제하면 된다.

```java
package exam01;

import java.util.ArrayList;

public class Ex01 {
    public static void main(String[] args) {
    ArrayList<String> names = new ArrayList<>();
    names.add("이름1");
    names.add("이름2");
    names.add("이름3");
    names.add("이름4");
    names.add("이름5");
  /*      for (int i = 0; i < names.size(); i++) {
            names.remove(i);
        }*/

        for (int i = names.size() -1; i >= 0 ; i--) {
            names.remove(i);
        }
        for (int i = 0; i < names.size(); i++) {
            String name = names.get(i);
            System.out.println(name);
        }

    }
}
```

- ArrayList **데이터 얻기**

:List에 담긴 값을 가져올 때는 E get(int index)메서드를 이용해 index 위치에 저장되어 있는 값을 출력할 수 있다.

<aside>
💡 List의 출력은 향상된 for문을 이용해 출력할 수도 있다.
for(int value : list) {
      System.out.println(”값 : “ + value);
}

</aside>

```java
package com.test01;

import java.util.*;

public class MTest01 {
    public static void main(String[] args) {
    	ArrayList<Integer> arrList = new ArrayList<Integer>();
    	 
    	// add() 메소드를 이용한 요소의 저장
    	arrList.add(40);
    	arrList.add(20);
    	arrList.add(30);
    	arrList.add(10);
    	 
    	// for 문과 get() 메소드를 이용한 요소의 출력
    	System.out.print("arrList에 들어 있는 값 : ");
    	for (int i = 0; i < arrList.size(); i++) {
    	    System.out.print(arrList.get(i) + " ");
    	}
  
    	System.out.println();
    	 
    	// remove() 메소드를 이용한 요소의 제거
    	arrList.remove(1);
    	// Enhanced for 문과 get() 메소드를 이용한 요소의 출력
		System.out.print("1번째 값이 제거된 후 남은 값 : ");
    	for (int e : arrList) {
    	    System.out.print(e + " ");
    	}

    	System.out.println();
    	 
    	// Collections.sort() 메소드를 이용한 요소의 정렬
    	Collections.sort(arrList);
    	// iterator() 메소드와 get() 메소드를 이용한 요소의 출력
    	System.out.print("정렬된 후 의 arrList : ")l
    	Iterator<Integer> iter = arrList.iterator();
    	while (iter.hasNext()) {
    	    System.out.print(iter.next() + " ");
    	}

    	System.out.println();
    	 
    	// set() 메소드를 이용한 요소의 변경
    	arrList.set(0, 20);
    	System.out.print("0번 값이 변경 된 후 arrList : ");
    	for (int e : arrList) {
    	    System.out.print(e + " ");
    	}
    	
    	System.out.println();
    	 
    	// size() 메소드를 이용한 요소의 총 개수
    	System.out.println("리스트의 크기 : " + arrList.size());
    }
}
```

<img src="https://github.com/somi9954/Java/assets/137499604/f139d82c-e1c1-44bf-b7e2-f3854b82b145" width="350">

### LinkedList

- 데이터와 다음 데이터의 주소를 가지는 노드(node)채가 연결되어 데이터를 저장하는 자료 구조이다.
- 속도는 ArrayList 보다 불리
- ArrayList와 마찬가지로 List 컬렉션의 구현 클래스이므로 사용할 수 있는 메서드가 대부분 동일하다.
- 불연속적으로 존재하는 데이터를 서로 연결(link)한 형태로 구성되어 있다.
- ArrayList는 배열을 이용해 데이터를 저장하는 반면에 LinkedList는  node라는 객체를 생성하여 인접  데이터를 링크해서 체인처럼 관리한다.
- 노드는 데이터 값과 주소를 가지는데, 주소는 다음에 오는 노드의 값을 가지고 있어서 연결 구조를 이룬다. 따라서 index가 실제 존재하지는 않지만 서로 연결되어 있기 때문에 순서를 알 수 있다.

<img src="https://github.com/somi9954/Java/assets/137499604/08f19076-892c-4dfe-a209-69e4866e9c72" width="350">

- LinkedList 생성자와 메소드는 다음과 같다.

| 생성자 또는 메서드 | 설명 |
| --- | --- |
| LinkedList() | LinkeList 객체를 생성 |
| LinkList(Collection c) | 주어진 컬렉션을 포함하는 LinkedList객체를 생성 |
| boolean add(Object o) | 지정된 객체(o)를 LinkedList의 끝에 추가, 저장에 성공하면 true, 실패하면 false |
| void add(int index, Object element) | 지정된 위치(index)에 객체(element)를 추가 |
| boolean addAll(Collection c) | 주저진 컬렉션에 포함된 모든 요소를 LinkedList의 끝에 추가한다. 성공하면 true, 실패하면 false) |
| void clear() | LinkedList의 모든 요소를 삭제 |
| boolean contains(Object o) | 지정된 객체가 LinkedList에 포함되어 있는지 알려줌 |
| boolean containsAll(Collection c) | 지정된 컬렉션의 모든 요소가 포함되어 있는지 알려줌 |
| Object get(int index) | 지정된 위치(index)의 객체를 반환 |
| int indexOf(Object o) | 지정된 객체가 저장된 위치(앞에서 몇 번째)를 반환 |
| boolean isEmpty() | LinkedList가 비어 있는지 알려 준다. 비어있으면 true |
| Iterator iterator() | Iterator를 반환한다. |
| int lastIndexOf(Object o) | 지정된 객체의 위치(index)를 반환(끝부터 역순검색) |
| ListIterator listIterator() | ListIterator를 반환한다. |
| ListIterator listIterator(int index) | 지정된 위치에서부터 시작하는 ListIterator를 반환 |
| Object remove(int index) | 지정된 위치(index)의 객체를 LinkedList에서 제거 |
| booleam remove(Object o) | 지정된 객체를 LinkedList에서 제거, 성공하면 true, 실패하면 false |
| boolean removeAll(Collection c) | 지정된 컬렉션의 요소와 일치하는 요소를 모두 삭제 |
| boolean retainAll(Collection c) | 지정된 컬렉션의 모든 요소가 포함되어 있는지 확인 |
| Object set(int index, Object element) | 지정된 위치(index)의 객체를 주어진 객체로 바꿈 |
| int size() | LinkedList에 저장된 객체의 수를 반환 |
| List subList(int fromIndex, int toIndex) | LinkedList의 일부를 List로 반환 |
| Object[] toArray() | LinkedList에 저장된 객체를 배열로 반환 |
| Object[] toArray(Object[] a) | LinkedList에 저장된 객체를 주어진 배열에 저장하여 반환 |
| Object element() | LinkedList의 첫 번째 요소를 반환 |
| boolean offer(Object o) | 지정된 객체(o)를 LinkedList의 끝에 추가, 성공하면 true, 실패하면 false |
| Object peek() | LinkedList의 첫 번째 요소를 반환 |
| Object poll() | LinkedList의 첫 번째 요소를 반환, LinkedList에서는 제거된다. |
| Object remove() | LinkedList의 첫 번째 요소를 제거 |
| void addFirst(Object o) | LinkeList의 맨 앞에 객체(o)를 추가 |
| void addLast(Object o) | LinkedList의 맨 끝에 객체(o)를 추가 |
| Iterator descendingIterator() | 역순으로 조회하기 위한 DescendingIterator를 반환 |
| Object getFirst() | LinkedList의 첫번째 요소를 반환 |
| Object getLast() | LinkedList의 마지막 요소를 반환 |
| boolean offerFirst(Object o) | LinkedList의 맨 앞에 객체(o)를 추가, 성공하면 true |
| boolean offerLast(Object o) | LinkedList의 맨 끝에 객체(o)를 추가, 성공하면 true |
| Object peekFirst() | LinkedList의 첫번째 요소를 반환 |
| Object peekLast() | LinkedList의 마지막 요소를 반환 |
| Object pollFirst() | LinkedList의 첫번째 요소를 반환하면서 제거 |
| Object pollLast() | LinkedList의 마지막 요소를 반환하면서 제거 |
| Object pop() | removeFirst()와 동일 |
| void push(Object o) | addFirst()와 동일 |
| Object removeFirst() | LinkedList의 첫번째 요소를 제거 |
| Object removeLast() | LinkedList의 마지막 묘소를 제거 |
| boolean removeFirstOccurence(Object o) | LinkedList에서 첫번째로 일치하는 객체를 제거 |
| boolean removeLastOccurence(Object o) | LinkedList에서 마지막으로 일치하는 객체를 제거 |

> LinkedList는 Queue인터페이스(JDK1.5)와 Deque인터페이스(JDK1.6)를 구현하도록 변경되었는데, 마지막 22개 메서드는 Queue인터페이스와 Deque 인터페이스를 구현하면서 추가된 것이다.
> 

- **LinkedList 선언**

```java
List<Integer> list = new LinkedList<Integer>();
List<Integer> list = new LinkedList<>();
또는
LinkedList<Integer> list = new LinkedList<Integer>();
LinkedList<Integer> list = new LinkedList<>();
```

LinkedList는 List 인터페이스 외 다른 기능들도 상속하고 있으므로 LinkedList 본연의 기능을 모두 사용할 경우에는 기본적인 객체 선언 방식을 선택한다.

- LinkedList **데이터 저장**

: add(int index, E e) 를 이용해 데이터를  추가한다. 하지만 내부적으로 동작하는 방식은 다르다

<img src="https://github.com/somi9954/Java/assets/137499604/cf081cd0-a500-42f0-9347-2ff9ad1c3d92" width="350">

데이터를 추가할 때는 기존에 연결되어 있던 링크를 끊고, 추가되는 데이터에 새로운 주소를 연결한다. 또한 추가되는 노드는 뒤에 올 데이터와 링크하여 삽입한다. 노드가 가지고 있는 다음에 오는 개체의 주소만 변경하면 되므로 빠르게 처리할 수 있다.

- LinkedList **삭제**

: remove(int index), remove(Object o) 메서드를 사용한다. List를 상속한 자료 구조들은 List 인터페이스를 상속하여 구현했으므로 사용 메서드는 동일하다. 삭제할 데이터와의 연결을 끊고 그 뒤의 데이터와 연결하여 쉽게 데이터를 삭제한다.

<img src="https://github.com/somi9954/Java/assets/137499604/d0efcaf9-b9ae-4bce-ad31-1c9d1a5e2864" widht="350">

```java

import java.util.LinkedList;
import java.util.List;
 
public class ListPractice {
    public static void main(String[] args) {
        List<String> list = new LinkedList<>();//컬렉션 인스턴스 생성
        
        list.add("Toy");
        list.add("Box");
        list.add("Robot");
        
        for(int i=0; i<list.size();i++) {
            System.out.println(list.get(i)+"\t");
        }
        System.out.println();
        
        list.remove(0);
        for(int i=0; i<list.size();i++) {
            System.out.println(list.get(i)+"\t");
        }
        System.out.println();
        
    }
}
```

<img src="https://github.com/somi9954/Java/assets/137499604/b1b45c7f-355c-46ea-8efc-b061f132d7c4" width="200">

*#enhanced for문 사용*

```java
import java.util.LinkedList;
import java.util.List;
 
public class ListPractice {
    public static void main(String[] args) {
        List<String> list = new LinkedList<>();//컬렉션 인스턴스 생성
        
        list.add("Toy");
        list.add("Box");
        list.add("Robot");
        
        for (String s : list) {
            System.out.println(s+"\t");
        }
        
    }
}
```

<img src="https://github.com/somi9954/Java/assets/137499604/657be441-19ba-43cb-969d-fc609133d10c" width="200">


Iterable<T> 인터페이스의 구현 덕분에 for each문을 사용할 수 있다.

collection<T>는 extends Iterable<T> 이기 때문에 다양한 자료구조로 부터 일정하게 참조 할 수 있다.

- ArrayList와 LinkedList 비교

```java
import java.util.ArrayList;
import java.util.LinkedList;

public class List3 {
    public static void main(String[] args) {
        // ArrayList 선언

        ArrayList<Integer> arrayList = new ArrayList<>();

        // LinkedList 선언
        LinkedList<Integer> linkedList = new LinkedList<>();

        // ArrayList 연속으로 데이터 추가
        long startTime = System.nanoTime();
        for(int i = 0; i < 1000000; i++) {
            arrayList.add(i);
        }

        long endTime = System.nanoTime();
        long duration = endTime - startTime;
        System.out.println("ArrayList 추가 시간 : " + duration);

        // LinkedList 연속으로 데이터 추가
        startTime = System.nanoTime();
        for(int i = 0; i < 1000000; i++) {
            linkedList.add(i);
        }
        endTime = System.nanoTime();
        duration = endTime - startTime;
        System.out.println("LinkedList 추가 시간 : " + duration);

        startTime = System.nanoTime();
        // ArrayList 선택적 삽입
        arrayList.add(99, 100);

        endTime = System.nanoTime();
        duration = endTime - startTime;
        System.out.println("ArrayList 삽입 시간 : " + duration);

        startTime = System.nanoTime();
        // LinkedList 선택적 삽입
        linkedList.add(99, 100);

        endTime = System.nanoTime();
        duration = endTime - startTime;
        System.out.println("LinkedList 삽입 시간 : " + duration);

        // ArrayList
        startTime = System.nanoTime();
        for(int i = 9999; i >=0; i--) {
            arrayList.remove(i);
        }
        endTime = System.nanoTime();
        duration = endTime - startTime;
        System.out.println("ArrayList 지우기 : " + duration);

        // LinkedList
        startTime = System.nanoTime();
        for(int i = 9999; i >=0; i--) {
            linkedList.remove(i);
        }
        endTime = System.nanoTime();
        duration = endTime - startTime;
        System.out.println("LinkedList 지우기 : " + duration);
    }
}
```

<img src="https://github.com/somi9954/Java/assets/137499604/dda09b80-2f22-45f6-91ce-5723fa99457c" width="200">

| 컬렉션 | 읽기(접근시간) | 추가/삭제 | 비고 |
| --- | --- | --- | --- |
| ArrayList | 빠르다 | 느리다 | 순차적인 추가삭제는 더 빠름.비효율적인 메모리사용 |
| LinkedList | 느리다 | 빠르다 | 데이터가 많을수록 접근성이 떨어진다. |

### Stack

- 마지막에 저장한 데이터를 가장 먼저 꺼내게 되는 LIFO(Last In First Out)구조로 되어 있다.
- ArrayList와 같은 배열 기반 클래스가 적합하다.
- Stack은 수식계산, 수식괄호검사, 워드프로세서의 undo/redo, 웹브라우저의 뒤로/앞으로 와 같은 곳에 활용이 된다
- Stack을 선언하는 방법은 다음과 같다

```java
Stack<Integer> st = new Stack<>();
```

- stack 클래스와 추가 된 메서드는 다음과 같다

| 소드 | 설명 |
| --- | --- |
| boolean empty() | 스택이 비어 있는지 여부를 조사한다. |
| E peek() | 스택의 맨 위에 저장된 객체를 반환한다. pop()와 달리 스택에서 객체를 꺼내지 않는다. (비었을때 EmptyStackException 발생) |
| E pop() | 스택의 맨 위에 저장된 객체를 반환한다. (비었을때 EmptyStackException 발생) |
| E push(E item) | 스택의 객체(item)을 저장한다. |
| int search(Object o) | 스택에서 주어진 객체(o)를 찾아서 그 위치를 반환한다. 못 찾으면 -1을 반환한다.(배열과 달리 위치는 0이 아닌 1부터 시작한다. 맨위의 요소가 1이다) |

```java
Stack<Integer> stack = new Stack<>(); //int형 스택 선언
stack.push(1);     // stack에 값 1 추가
stack.push(2);     // stack에 값 2 추가
stack.size();      // stack의 크기 출력 : 2
stack.empty();     // stack이 비어있는제 check (비어있다면 true)
stack.contains(1) // stack에 1이 있는지 check (있다면 true)
```

### Vector

- ArrayList와 거의 동일 하다.
- Object[] 배열을 사용하여 요소 접근에서 빠른 성능을 보인다.
- 항상 동기화(여러 쓰레드가 동시에 데이터에 접근하려면 순차적으로 처리한다) 되기 때문에  멀티 쓰레드에서 안전하지만 단일 쓰레이드에서는 동기화를 하기 때문에  ArrayList에 비해 성능이 약간 느리다.
- 구버전 자바와 호환성을 위해 남겨두었으며 잘 쓰이진 않는다.
- 초기 배열 크기를 지정하지 않으면 **초기 배열의 크기(initial capacity)는 10**이다.
- 초기 배열 크기 증가 값을 지정하지 않으면 **배열의 크기가 2배씩 커진다**.
- Vector을 선언하는 방법은 다음과 같다

```java
Vector<Integer> vector1 = new Vector<Integer>(); // 타입 지정
Vector<Integer> vector2 = new Vector<>(); // 타입 생략 가능
Vector<Integer> vector3 = new Vector<>(10); // 초기 용량(Capacity) 설정
Vector<Integer> vector4 = new Vector<>(10, 10); // 초기 용량, 증가량 설정
Vector<Integer> vector5 = new Vector<>(vector1); // 다른 Collection값으로 초기화
Vector<Integer> vector6 = new Vector<>(Arrays.asList(1, 2, 3, 4, 5)); // Arrays.asList()
```

<aside>
💡 만일 현업에서 컬렉션에 동기화가 필요하면 Collections.synchronizedList()메서드를 이용해 ArrayList를 동기화 처리해서 사용한다.

</aside>

- ArrayList와는 다른점으로  capacity()메소드를 통해서 배열의 크기를 알 수 있다.

```java
import java.util.Vector;

public class test5 {
    public static void main(String[] args)  {
        Vector V = new Vector();

        V.add("Hello");
        V.add("World");
        V.add("Hello");
        V.add("World");

        System.out.println("Size : " + V.size()); // Vector의 크기 구하기
        System.out.println("Capacity : " + V.capacity()); // Vector의 용량 구하기
    }
}
```

<img src="https://github.com/somi9954/Java/assets/137499604/09ef6ce4-ef07-4a60-a298-06f8658897c3" width="200">


### ⭐정리

**데이터 추가**
add(....)
add(int index, E e)

addAll(Collection<E> …)

**데이터 조회**
		E get(int index) : 순서 번호로 조회
		boolean contains(Object o) : 특정 요소가 존재 하면 true

                boolean contaiinsAll(Collection<E> …) → 인자로 주어진 컬렉션과 모두 일치해야 true를

                반환한다. 일부만 일치하면 false를 반환한다.
		int indexOf(Object o) : 특정 요소가 있는 위치 값 반환(0부터 시작)
							  - 없으면 -1 반환
							  - 왼쪽 -> 오른쪽

		int lastIndexOf(Object o) : 특정 요소가 있는 위치 값 반환
							- 없으면 -1반환
							- 오른쪽 -> 왼쪽

		int size() : 요소의 갯수

**데이터 삭제**
		E remove(int index) : 순서 번호로 요소 삭제
		remove(Object o)

                boolean remove(Objcet o)

**데이터 변경**
		E set(int index, E e)
