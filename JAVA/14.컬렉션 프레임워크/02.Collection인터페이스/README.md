# 컬렉션 클래스(collection class)

- 컬렉션 프레임워크에 속하는 인터페이스를 구현한 클래스를 컬렉션 클래스(collection class)라고 합니다.
- 컬렉션 프레임워크의 모든 컬렉션 클래스는 List와 Set, Map 인터페이스 중 하나의 인터페이스를 구현하고 있습니다.
- 또한, 클래스 이름에도 구현한 인터페이스의 이름이 포함되므로 바로 구분할 수 있습니다.
- Vector나 Hashtable과 같은 컬렉션 클래스는 예전부터 사용해 왔으므로, 기존 코드와의 호환을 위해 아직도 남아 있다. 하지만 통일성이 없었고 표준화된 인터페이스가 존재하지 않는다.
- 하지만 기존에 사용하던 컬렉션 클래스를 사용하는 것보다는 새로 추가된 ArrayList나 HashMap 클래스를 사용하는 것이 성능 면에서도 더 나은 결과를 얻을 수 있습니다.

# Collection인터페이스

- Collection은 List와 Set의 상위 인터페이스이다.
- Collection 인터페이스는 컬렉션 클래스에 저장된 데이터를 읽고, 추가하고, 삭제하는 등 컬렉션을 다루는데 가장 기본이적인 메서드들을 정의하고 있다.

### Collection 인터페이스에 정의된 메서드

| 메서드 | 설명 |
| --- | --- |
| boolean add(Object o)boolean addAll(Collection c) | 지정된 객체(o) 또는 Collection(c)의 객체들을 Collection에 추가한다. |
| void clear() | Collection의 모든 객체를 삭제한다. |
| boolean contains(Object o)boolean containsAll(Collection c) | 지정된 객체(o) 또는 Collection의 객체들이 Collection에 포함되어 있는지 확인한다. |
| boolean equals(Object o) | 동일한 Collection인지 비교한다. |
| int hashCode() | Collection의 hash code를 반환한다. |
| boolean isEmpty() | Collection이 비어 있는지 확인한다. |
| Iterator iterator() | Collection의 iterator를 얻어서 반환한다. |
| boolean remove(Object o) | 지정된 객체를 삭제한다. |
| boolean removeAll(Collection c) | 지정된 Collection에 포함된 객체들을 삭제한다. |
| boolean retainAll(Collection c) | 지정된 Collection에 포함된 객체만 남기고 다른 객체들은 Collection에서 삭제한다. 이 작업으로 인해 Collection에 변화가 있으면 true를 그렇지 않다면 false를 반환한다. |
| int size() | Collection에 저장된 객체의 개수를 반환한다. |
| Object[] toArray() | Collection에 저장된 객체를 객체배열(Object[])로 반환한다. |
| Object[] toArray(Object[] a) | 지정된 배열에 Collection의 객체를 지정해서 반환한다. |

# Collections란?

- Collection인터페이스와 달리 Java 1.2이상부터 Collections라는 static클래스가 존재합니다.
- Collections 는 컬렉션 프레임웍에 속하는 클래스를 지원해주는 다양한 메소드가 존재합니다.

### Collections 클래스의 메소드

| Collections.sort(List L) | 리스트를 정렬합니다. |
| --- | --- |
| Collections.sort(List L , reverseOrder()) | 리스트를 역순으로 정렬합니다. |
| max(List L) , min(List L) | 리스트에서 최대 최솟값 |
| shuffle(List L) | 리스트를 랜덤으로 섞음 |
| binarySearch(List L , Key) | 오름차순으로 정렬된 리스트에서 이진검색을 통해 위치를 반환, 실패시 -1반환 |
| disjoint(List L1 , List L2) | 두 리스트의 값이 완전히 다른지 검사 , 하나라도 같은값이 있으면 False |

```java
import java.util.*;
import static java.util.Collections.*;

class Ex11_19 {
	public static void main(String[] args) {
		List list = new ArrayList();
		System.out.println(list);

		addAll(list, 1,2,3,4,5); 
		System.out.println(list);
		
		rotate(list, 2);  // 오른쪽으로 두 칸씩 이동 
		System.out.println(list);

		swap(list, 0, 2); // 첫 번째와 세 번째를 교환(swap)
		System.out.println(list);

		shuffle(list);    // 저장된 요소의 위치를 임의로 변경 
		System.out.println(list);

		sort(list, reverseOrder()); // 역순 정렬 reverse(list);와 동일 
		System.out.println(list);
		
		sort(list);       // 정렬 
		System.out.println(list);
 
		int idx = binarySearch(list, 3);  // 3이 저장된 위치(index)를 반환
		System.out.println("index of 3 = " + idx);
		
		System.out.println("max="+max(list));
		System.out.println("min="+min(list));
		System.out.println("min="+max(list, reverseOrder()));

		fill(list, 9); // list를 9로 채운다.
		System.out.println("list="+list);

		// list와 같은 크기의 새로운 list를 생성하고 2로 채운다. 단, 결과는 변경불가
		List newList = nCopies(list.size(), 2); 
		System.out.println("newList="+newList);

		System.out.println(disjoint(list, newList)); // 공통요소가 없으면 true

		copy(list, newList); 
		System.out.println("newList="+newList);
		System.out.println("list="+list);

		replaceAll(list, 2, 1); 
		System.out.println("list="+list);

		Enumeration e = enumeration(list);
		ArrayList list2 = list(e); 

		System.out.println("list2="+list2);
	}
}
```

<img src="https://github.com/somi9954/Java/assets/137499604/2b2712c0-8e9f-409e-b68e-d6cb8435b190" width="200">

[Collections 추가 메서드](https://codevang.tistory.com/139)
