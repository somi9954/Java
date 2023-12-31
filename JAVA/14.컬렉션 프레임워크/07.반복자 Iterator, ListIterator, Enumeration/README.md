## Iterator - 표준화

- Iterator는 자바의 컬렉션 프레임워크에서 컬렉션에 저장되어있는 요소들을 읽어오는 방법 중 하나다.
- Collection 인터페이스에는 iterator()라는 메소드가 정의되어 있다.
- iterator 메소드가 반환하는 참조 값의 인스턴스는 Iterator 인터페이스를 구현하고 있다.
- itertaor 메소드가 반환하는 참조값의 인스턴스를 이용하면, **컬렉션 인스턴스에 저장된 인스턴스의 순차적 접근이 가능함**.
- iterator 메소드가 반환형이 Iterator 이니, 반환된 참조값을 이용해서 Iterator에 선언된 함수들만 호출하면 된다.

**Iterator 인터페이스에 정의된 메소드**

```java
- boolean hasNext() : 참조할 다음 번 요소 (element)가 존재하면 true를 반환
- E next() : 다음 번 요소를 반환
- void remove() : 현재 위치의 요소를 삭제
```

반복을 다하면 종료하여 재활용이 불가하다.

**사용 예시**

```java

public class test10 {
    public static void main(String[] args) {
        LinkedList list = new LinkedList();
        list.add("First");
        list.add("Second");
        list.add("Third");
        list.add("Fourth");

        Iterator<String> itr = list.iterator();

        System.out.println("반복자를 이용한 1차 출력과 Third 삭제");
        while(itr.hasNext()){
            String curStr = itr.next();
            System.out.println(curStr);
            if(curStr.compareTo("Third")==0)
                itr.remove();
        }

        System.out.println("Third 삭제 후 반복자를 이용한 2차 출력");
        itr = list.iterator();
        while(itr.hasNext())
            System.out.println(itr.next());

    }
}

```

<img src="https://github.com/somi9954/Java/assets/137499604/2bc33f75-e73e-4765-9605-79aee08a6769" width="350">


```java
//List의 Iterator
package section16;
import java.util.Arrays;
import java.util.Iterator;
import java.util.List;

public class EX16_12 {
	public static void main(String[] args) {
		
		List<Integer> list = Arrays.asList(1,2,3,4,5,6,7,8,9,10);
		// Iterator 객체 가져오기
		Iterator<Integer> iter = list.iterator();
		int count = 0;
		// 반환할 요소가 있는지 검사
		while(iter.hasNext()) {
			// 요소 반환
			int val = iter.next();
			System.out.println("list 데이터[" + (count++) + "] : " + val);
		}
	}
}
```

<img src="https://github.com/somi9954/Java/assets/137499604/3e6bcf2b-72c7-4bb2-8b9e-fe0656c6c15c" width="350">

```java
//Set의 Iterator
package section16;
import java.util.HashSet;
import java.util.Iterator;
import java.util.Set;

public class EX16_13 {
	public static void main(String[] args) {
		
		Set<Integer> set = new HashSet< >();
		// 데이터 삽입
		for(int i = 1; i <= 10; i++) {
			set.add(i);
		}
		// Iterator 객체 가져오기
		Iterator<Integer> iter = set.iterator();
		
		int count = 0;
		// 반환할 요소가 있는지 검사
		while(iter.hasNext()) {
			// 요소 반환
			int val = iter.next();
			System.out.println("set 데이터["+ (count++) +"] : " + val);
		}
	}
}
```

<img src="https://github.com/somi9954/Java/assets/137499604/c712ebef-0cd0-40b0-9199-d111fe438869" width="350">

```java
//map의 Iterator
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;

public class MapIterationSample {
    public static void main(String[] agrs) {
        Map<String, String> map = new HashMap<String, String>();

        map.put("키1", "값1");
        map.put("키2", "값2");
        map.put("키3", "값3");
        map.put("키4", "값4");
        map.put("키5", "값5");
        map.put("키6", "값6");

        // 방법1
        Iterator<String> keys = map.keySet().iterator();
        while( keys.hasNext() ){
            String key = keys.next();
            System.out.println( String.format("키 : %s, 값 : %s", key, map.get(key)) );
        }
        System.out.println("--------------------------------------------------------");
        // 방법2
        for( Map.Entry<String, String> elem : map.entrySet() ){
            System.out.println( String.format("키 : %s, 값 : %s", elem.getKey(), elem.getValue()) );
        }
        System.out.println("--------------------------------------------------------");
        // 방법3
        for( String key : map.keySet() ){
            System.out.println( String.format("키 : %s, 값 : %s", key, map.get(key)) );
        }
    }
}
```

- Map 인터페이스를 구현한 컬렉션 클래스는 키(key)와 값(value)을 쌍(pair)으로 저장하고 있기 때문에 iterator()를 직접 호출할 수 없다.
- 그 대신 keySet()이나 entrySet()과 같은 메서드를 통해서 키와 값을 각각 따로 Set의 형태로 얻어 온 후에 다시 iterator()를 호출해야 Iterator를 호출해야 Iterator를 얻을 수 있다.

```java
키 : 키1, 값 : 값1
키 : 키3, 값 : 값3
키 : 키2, 값 : 값2
키 : 키5, 값 : 값5
키 : 키4, 값 : 값4
키 : 키6, 값 : 값6
--------------------------------------------------------
키 : 키1, 값 : 값1
키 : 키3, 값 : 값3
키 : 키2, 값 : 값2
키 : 키5, 값 : 값5
키 : 키4, 값 : 값4
키 : 키6, 값 : 값6
--------------------------------------------------------
키 : 키1, 값 : 값1
키 : 키3, 값 : 값3
키 : 키2, 값 : 값2
키 : 키5, 값 : 값5
키 : 키4, 값 : 값4
키 : 키6, 값 : 값6
```

## ListIterator 인터페이스

- Iterator 인터페이스를 상속 받아 여러 기능을 추가한 클래스
- Iterator 인터페이스는 컬렉션의 요소에 접근할 때 한 방향으로만 이동할 수 있다.
- 하지만 JDK 1.2부터 제공된 ListIterator 인터페이스는 컬렉션 요소의 대체, 추가 그리고 인덱스 검색 등을 위한 작업에서 양방향으로 이동하는 것을 지원한다.
- 단, ListIterator 인터페이스는 List 인터페이스를 구현한 List 컬렉션 클래스에서만 listIterator() 메소드를 통해 사용할 수 있다.
- ListIterator의 메소드는 다음과 같다.

| 리턴 타입 | 메소드 | 설명 |
| --- | --- | --- |
| void | add(E e) | 해당 리스트(list)에 전달된 요소를 추가함. (선택적 기능) |
| boolean | hasNext() | 이 리스트 반복자가 해당 리스트를 순방향으로 순회할 때 다음 요소를 가지고 있으면 true를 반환하고, 더 이상 다음 요소를 가지고 있지 않으면 false를 반환함. |
| boolean | hasPrevious() | 이 리스트 반복자가 해당 리스트를 역방향으로 순회할 때 다음 요소를 가지고 있으면 true를 반환하고, 더 이상 다음 요소를 가지고 있지 않으면 false를 반환함. |
| E | next() | 리스트의 다음 요소를 반환하고, 커서(cursor)의 위치를 순방향으로 이동시킴. |
| int | nextIndex() | 다음 next() 메소드를 호출하면 반환될 요소의 인덱스를 반환함. |
| E | previous() | 리스트의 이전 요소를 반환하고, 커서(cursor)의 위치를 역방향으로 이동시킴. |
| int | previousIndex() | 다음 previous() 메소드를 호출하면 반환될 요소의 인덱스를 반환함. |
| void | remove() | next()나 previous() 메소드에 의해 반환된 가장 마지막 요소를 리스트에서 제거함. (선택적 기능) |
| void | set(E e) | next()나 previous() 메소드에 의해 반환된 가장 마지막 요소를 전달된 객체로 대체함. (선택적 기능) |

```java
LinkedList<Integer> list = new LinkedList<Integer>();

list.add(1);
list.add(2);
list.add(3);
list.add(4);
 
ListIterator<Integer> iter = list.listIterator();
while (iter.hasNext()) {
    System.out.print(iter.next() + " ");
}
 
while (iter.hasPrevious()) {
    System.out.print(iter.previous() + " ");
}

출력값
1 2 3 4
4 3 2 1
```

## ****Enumeration****

- Enumeration<E>과 Iterator<E>는 객체들을 집합체 형태로 관리하게 해주는 인터페이스다.
- 이 인터페이스에는 각각의 객체들을 한 번에 하나씩 처리할 수 있는 메소드를 제공 한다.
- 논리적인 커서가 존재하여 커서를 이동하면서 데이터를 꺼내온다.
- 데이터를 삭제하는 기능이 없어 HashTable와 Vector에 사용이 가능하다.
- Enumeration과 함께 쓰이는 메소드는 다음과 같다.

      1) boolean hasMoreElements() : boolean 타입을 반환

 현재 커서 이후에 요소들이 있는지 여부를 체크한다.
요소가 있으면 true, 없으면 false를 반환한다.
(맨처음 커서는 첫번째 요소 직전에 위치)

      2) E nextElement() :

       E 타입을 반환(E는 Enumeration 객체를 생성할 때 쓰는 타입과 동일하게 지정한다.)

커서를 다음 요소로 이동 시키고, 가리키고 있는 요소 객체를 꺼내 반환한다.

### **Vector에서 Enumeration 사용 방법**

1. Integer 유형을 담을 Vector 객체를 생성하고 데이터를 삽입한다.

```java
import java.util.*;

publicclassMain {

publicstaticvoidmain(String[] args) {
		Vector<Integer> v =new Vector<>();
		v.add(3);
		v.add(12);
		v.add(51);
	}

}
```

2. Enumeration<E> 객체를 생성한다. 이 때 Enumeration은 인터페이스 이므로 직접적으로 객체를 생성할 수 없다. 따라서 Enumeration 객체 타입으로 반환해주는 v.elements() 메소드를 사용해준다.

Vetor<Integer> 와 같이 Enumeration<E> 도 <Integer> 로 지정한다.

```java
Enumeration<Integer> em = v.elements();
```

3. hasMoreElemtets() 메소드와 nextElement() 메소드를 이용해서 데이터를 출력해보자

```java
// 현재 커서 이후에 요소들이 있는지 여부 체크, 있으면 true
while(em.hasMoreElements()) {
			// 해당 데이터를 가져오고 커서가 다음 요소를 가리키게 한다.
int val = em.nextElement();
			System.out.println(val);

}
```

```java
3
12
51

```

- **상세설명**

1) 처음 반복문에 들어갈 때 em.hasMoreElemtets() 가 현재 커서 이후에 요소들이 있는지 여부를 체크한다.

맨 처음 커서는 첫 번째 요소 앞에 출발점에 있다.

2) 우리는 요소(데이터)를 3개 저장했으니 현재 커서(첫 번째 요소 앞) 이후에 요소가 있으므로 true가 되며 반복문에 들어간다.

3) em.nextElement() 메소드를 통해 해당 요소를 꺼내고 현재 커서를 다음 요소를 가르키게 한다.

4) System.out.println(val)를 통해 첫 번째 요소를 출력한다.

5) 반복문을 통해 hasMoreElements() 메소드에서 커서가 다음 요소를 가리킬게 없다면 false가 되어 반복문이 종료된다.

```java
package algo;

import java.util.ArrayList;
import java.util.Collections;
import java.util.Enumeration;

public class test {
	public static void main(String[] args) {
		ArrayList<String> text = new ArrayList<String>();
		
		text.add("apple");
		text.add("banana");
		text.add("melon");
		text.add("watermelon");
		
		// Enumeration
		Enumeration<String> te = Collections.enumeration(text);
		
		// 출력
		while(te.hasMoreElements()) { // 다음 element가 있으면 true, 없으면 false를 반환
			System.out.println(te.nextElement());
		}
	}
}
```

```java
출력값
apple
banana
melon
watermelon
```

### **Java StAX (Streaming API for XML)**

- XML 파일 포맷을 읽거나 만들때 사용하는 자바 라이브러리
- 콘솔 기반의 API, 이터레이터 기반의 API를 제공한다.
    - **이터레이터 기반의 API** : xml의 Element마다 이벤트가 지나가면서 캡쳐하며 그 영역을 표현하는 XMLEvent라는 인스턴스가 새로 만들고 이를 이용하는 방식이다. (XmlEventReader, XmlEventWriter)
    - **콘솔 기반의 API** : 하나의 인스턴스가 Element를 지나가면서 직접 안의 내용들을 변경하는 방식이다. 그래서 메모리는 이터레이터 기반보다 효율적이지만 재사용, 변경 측면에서는 좋지 않아 이터레이터 기반의 API를 사용하는 것이 권장된다.
- 비슷한 SAX(Simple API for XML)도 있지만, SAX는 XML을 읽기만 가능하다.

이터레이터 기반의 API 코드 예제는 다음과 같다.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<books>    <book title="오징어 게임"/> 
 <book title="숨바꼭질"/>
    <book title="우리집에 왜 왔니"/>
</books>
```

```java
public static void main(String[] args) throws FileNotFoundException, XMLStreamException {
// 1. XMLEventReader 객체를 만드는 팩토리 객체를 얻는다.    
XMLInputFactory xmlInputFactory = XMLInputFactory.newInstance();
// 2. XMLEventReader 객체를 만든다.    
XMLEventReader reader = xmlInputFactory.createXMLEventReader(new FileInputStream("book.xml"));
// 3. 이터레이터 순회한다.    
while(reader.hasNext()) {
// <books> 엘리먼트를 캡쳐하여 그 영역을 표현하는 XMLEvent 인스턴스를 생성        
XMLEvent nextEvent = reader.nextEvent();
// 엘리먼트에 자식 엘리먼트가 있을 경우        
if(nextEvent.isStartElement()) {StartElement startElement = nextEvent.asStartElement();// <book>           
 QName name = startElement.getName();            
if(name.getLocalPart().equals("book")) {
// 엘리먼트의 속성을 얻는다. <book title=""/>               
 Attribute title = startElement.getAttributeByName(new QName("title"));                System.out.println(title.getValue());            
                           }        
								   }
				   }
	   }
```

<img src="https://github.com/somi9954/Java/assets/137499604/6f46190d-b97e-42b8-a205-6a931ebd3605" width="350">

### 반복자를 사용하는 이유

- 반복자를 사용하면, **컬렉션 클래스의 종류에 상관없이 동일한 형태의 데이터 참조 방식을 유지할** 수 있음.
- 컬렉션의 내부 구조 및 순회 방식을 알지 않아도 된다
- 컬렉션 클래스 교체에 큰 영향이 없음
- 컬렉션 클래스 별 데이터 참조 방식을 별도로 확인할 필요 없음

<img src="https://github.com/somi9954/Java/assets/137499604/840cb473-55ac-4514-b410-c14f31edb6b6" width="450">
