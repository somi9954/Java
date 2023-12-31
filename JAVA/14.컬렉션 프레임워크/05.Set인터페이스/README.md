# Set 인터페이스(집합 자료구조)

- 객체의 저장 순서를 저장하지 않는다.(인덱스로 객체를 검색해서 가져오는 get(index)메서드도 존재하지 않는다)
- 수학의 집합과 유사한 개념을 지니고 있다.
- 중복을 허용하지 않는다. null값도 하나만 저장이 가능하다.
- 구현 클래스에는 HashSet, TreeSet,LinkedHashSet이 있다.

<img src="https://github.com/somi9954/Java/assets/137499604/b688f8d4-3f75-4e0f-9718-d270f8e40285" width="450">

| 메서드 | 설명 |
| --- | --- |
| boolean add(E e) | 주어진 객체를 저장 후 성공적이면 true를 중복 객체면 false를 리턴합니다. |
| boolean contains(Object o) | 주어진 객체가 저장되어있는지 여부를 리턴합니다. |
| Iterator<E> iterator() | 저장된 객체를 한번씩 가져오는 반복자를 리턴합니다. |
| isEmpty() | 컬렉션이 비어있는지 조사합니다. |
| int Size() | 저장되어 있는 전체 객체수를 리턴합니다. |
| void clear() | 저장된 모든 객체를 삭제합니다. |
| boolean remove(Object o) | 주어진 객체를 삭제합니다. |

### **HashSet 클래스**

<img src="https://github.com/somi9954/Java/assets/137499604/3819e484-c017-4292-b9c6-053ec73be1bf" width="450">

- 배열과 연결 노드를 결합한 자료구조 형태
- 가장 빠른 임의 검색 접근 속도를 가진다
- 추가, 삭제, 검색, 접근성이 모두 뛰어나다
- 대신 순서를 전혀 예측할 수 없다
- 선언하는 방법은 다음과 같다.

```java
Set<E> set = new HashSet<E>();
Set<E> set = new HashSet<>();
```

- Hashset은 데이터를 저장할 때 순서를 부여하지 않고 데이터의 중복을 허용하지 않는다. 즉 동일한 값 또는 객체를 허용하지 않는다는 의미이다.
- HashSet은 데이터를 객체의 hashcode()값을 호출하여 비교하고 같으면 equals()메소드를 호출하여 다시 비교해 두 객체가 같음을 증명해야 한다.

<img src="https://github.com/somi9954/Java/assets/137499604/8869bf4c-a43a-4cef-b9a7-f131d9d6d324" width="450">

- hashset에 객체를 저장해야 한다면 해당 객체는 hashcode와 equals 메서드를 사용해 비교하는 로직을 구현해야 한다.

```java
import java.util.HashSet;
import java.util.Iterator;
import java.util.Set;

public class HashSetExam {
public static void main(String[] args) {
        Set<String> set = new HashSet<String>();
 
        set.add("Java");
        set.add("JDBC");
        set.add("JTBC");
        set.add("Java");
        set.add("iBATIS");
 
        int size = set.size();
        System.out.println("총 객체 수: " + size);
 
        Iterator<String> iterator = set.iterator();
 
        while (iterator.hasNext()) {
            String elem = iterator.next();
 
            System.out.println("\t" + elem);
        }
 
        set.remove("JDBC");
        set.remove("JTBC");
 
        System.out.println("총 객체 수: " + set.size());
 
        iterator = set.iterator();
 
        while (iterator.hasNext()) {
            String elem = iterator.next();
 
            System.out.println("\t" + elem);
        }
 
        set.clear();
 
        if (set.isEmpty())
            System.out.println("HashSet 비어있음");
    }
 
}
```

<img src="https://github.com/somi9954/Java/assets/137499604/3a3675bc-afd2-45df-821d-f9426e2f91c9" width="200">

### **LinkedHashSet 클래스**

- 순서를 가지는 Set 자료
- 추가된 순서 또는 가장 최근에 접근한 순서대로 접근 가능
- 만일 중복을 제거하는 동시에 저장한 순서를 유지하고 싶다면, HashSet 대신 LinkedHashSet을 사용하면 된다

```java
Set<Integer> linkedHashSet = new LinkedHashSet<>();
linkedHashSet.add(10);
linkedHashSet.add(20);
linkedHashSet.add(30);
linkedHashSet.add(10);// 중복된 수 추가

linkedHashSet.size();// 3 - 중복된건 카운트 X
linkedHashSet.toString();// [10, 20, 30] - 대신 자료가 들어온 순서대로 출력
```

### **TreeSet 클래스**

<img src="https://github.com/somi9954/Java/assets/137499604/e72f844b-58d1-4072-a237-a63f02fb96e0" widht="360">

- 이진 검색 트리(binary search tree) 자료구조의 형태로 데이터를 저장
- 중복을 허용하지 않고, 순서를 가지지 않는다
- 대신 데이터를 정렬하여 저장하고 있다는 특징이다
- 정렬, 검색, 범위 검색에 높은 성능을 뽐낸다.


```java
Set<Integer> treeSet = new TreeSet<>();
treeSet.add(7);
treeSet.add(4);treeSet.add(9);
treeSet.add(1);treeSet.add(5);
treeSet.toString();// [1, 4, 5, 7, 9] - 자료가 알아서 정렬됨
```

- 이진 검색 트리에 7, 4, 9, 1, 5의 순서로 값을 저장 순서

<img src="https://github.com/somi9954/Java/assets/137499604/fa36870d-0ee3-4a76-b10d-f784661a32f9" width="450">

```java
public class SetTest {
    public static void main(String[] args) {
        // create new Set
        Set<String> s1 = new HashSet<>();
        Set<String> s2 = Set.of("three", "four");

        // add element to Set
        s1.addAll(Arrays.asList("one", "two"));
        s1.addAll(s2);
        s1.add("five");
        s1.add("two");
        s1.remove("five");

        System.out.println("## element in Set");
        System.out.println(s1);

        // print all elements using stream api
        s1.stream().forEach(System.out::println);

        System.out.println("## check exist element in Set");
        System.out.println(s1.contains("one"));

        // create new LinkedHashSet and add elements
        Set<String> lset = new LinkedHashSet<>();
        lset.addAll(Arrays.asList("one", "two", "three", "four"));
        lset.add("five");

        System.out.println("\n## element in LinkedHashSet");
        System.out.println(lset);

        // get Iterator from LinkedHashSet
        System.out.println("## print element using Iterator");
        Iterator<String> iter = lset.iterator();
        while (iter.hasNext()) {
            System.out.println(iter.next());
        }

        // create new TreeSet and add elements
        Set<Integer> tset = new TreeSet<>();
        tset.addAll(Arrays.asList(50, 10, 60, 20));

        System.out.println("\n## elements in TreeSet");
        System.out.println(tset);

        // Descending sort with stream api
        System.out.println("## Descending sort with stream api");
        tset.stream().sorted((o1, o2) -> o2.toString().compareTo(o1.toString())).forEach(System.out::println);
    }
}
```

```java
## element in Set
[four, one, two, three]
four
one
two
three
## check exist element in Set
true

## element in LinkedHashSet
[one, two, three, four, five]
## print element using Iterator
one
two
three
four
five

## elements in TreeSet
[10, 20, 50, 60]
## Descending sort with stream api
60
50
20
10
```

### **EnumSet 추상 클래스**

- **[EnumVisit Website](https://inpa.tistory.com/entry/JAVA-%E2%98%95-%EC%97%B4%EA%B1%B0%ED%98%95Enum-%ED%83%80%EC%9E%85-%EB%AC%B8%EB%B2%95-%ED%99%9C%EC%9A%A9-%EC%A0%95%EB%A6%AC)** 클래스와 함께 동작하는 Set 컬렉션이다
- 중복 되지 않은 상수 그룹을 나타내는데 사용된다
- 산술 비트 연산을 사용하여 구현되므로 HashSet 보다 훨씬 빠르며, 적은 메모리를 사용한다
- 단, enum 타입의 요소값만 저장할 수 있고, 모든 요소들은 동인한 enum 객체에 소속되어야 한다
- EnumSet은 추상 클래스고 이를 상속한 RegularEnumSet 혹은 JumboEnumSet 객체를 사용하게 된다.

```java
enum Color {    RED, YELLOW, GREEN, BLUE, BLACK, WHITE}
public class Client {    
	    public static void main(String[]args) {
// 정적 팩토리 메서드를 통해 RegularEnumSet 혹은 JumboEnumSet 을 반환
// 만일 enum 상수 원소 갯수가 64개 이하면 RegularEnumSet, 
//이상이면 JumboEnumSet 객체를 반환       
 EnumSet<Color> enumSet = EnumSet.allOf(Color.class);
        for (Color color : enumSet) {  
          System.out.println(color); }        
        enumSet.size();// 6       
        enumSet.toString();// [RED, YELLOW, GREEN, BLUE, BLACK, WHITE]    }}
```

### ⭐정리
```java
데이터 추가

add(E e)

addAll(Collection<E>… )

데이터 조회

boolean contains(Object o)

boolean containsAll(Collection<E> ...)

데이터 제거

remove(Object o)

removeAll(Collection<E>...)

기타
int size()       : 요소 갯수
boolean isEmpty() : 요소가 비어있는 상태인지
clear()          : 전체 비우기
```
