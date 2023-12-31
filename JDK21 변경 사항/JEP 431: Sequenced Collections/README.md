# JEP 431: Sequenced Collections


* 기존의 자바 컬렉션 프레임워크는 정해진 순서의 원소에 접근하는 것이 어려웠다.
* 예를 들어 List와 Deque는 모두 처음과 마지막 원소에 접근할 수 있지만, 이들의 공통 상위 인터페이스는 Collection라서 접근 방법이 다르다.
* SortedSet과 LinkedHashSet 역시 비슷한데, 이로 인해 다음과 같이 일관되지 못한 방법으로 원소에 접근하게 되는 것이다.

|     |First element|Last element|
|------|---|---|
|List|list.get(0)|list.get(list.size() - 1)|
|Deque|deque.getFirst()|deque.getLast()|
|SortedSet|sortedSet.first()|sortedSet.last()|
|LinkedHashSet|linkedHashSet.iterator().next()|// missing|

* Java 21부터는 정해진 순서의 원소를 조회할 수 있는 컬렉션을 표현하는 새로운 인터페이스를 도입한다. 이를 통해 정해진 순서의 원소(첫 원소와 마지막 원소 등)에 접근하고, 이를 역순으로 처리하기 위한 일관된 API를 제공한다.

![image](https://blog.kakaocdn.net/dn/mFbfx/btstLPvwi7c/LTHKsXVqdKu0Bd7alxbvp1/img.png)

### SequencedCollection
* SequencedCollection은 처음과 마지막 요소에 대한 공통된 기능을 제공한다. reversed()는 새롭게 추가된 메소드이지만, 나머지는 Deque로부터 승격된 것이다.

```JAVA
interface SequencedCollection<E> extends Collection<E> {
    // new method
    SequencedCollection<E> reversed();
    // methods promoted from Deque
    void addFirst(E);
    void addLast(E);
    E getFirst();
    E getLast();
    E removeFirst();
    E removeLast();
}
```
* 추가로 제공되는 reversed()는 기존 컬렉션에서 역순으로 원소들을 처리할 수 있게 된다. 예를 들어 iterator()나 forEach(), stream(), parallelStream(), toArray() 등과 같은 기능을 역순 상태의 원소로 호출 가능해지는 것이다.

```JAVA
linkedHashSet.reversed().stream()
```
### SequencedSet
* SequencedSet은 중복된 원소를 갖지 않는 SequencedCollection에 해당하는 Set이다. SortedSet과 같은 컬렉션은 SequencedCollection 부모 인터페이스에 선언된 addFirst(E) 및 addLast(E) 메소드 등을 지원할 수 없기 때문에 UnsupportedOperationException을 던질 수 있다.

```JAVA
interface SequencedSet<E> extends Set<E>, SequencedCollection<E> {
    SequencedSet<E> reversed();    // covariant override
}
```
* addFirst(E)와 addLast(E)는 LinkedHashSet과 같은 구현체에 특별한 의미를 갖는다. 왜냐하면 원소가 이미 존재하는 경우에 적절한 위치로 재배치되기 때문이다. 이는 요소를 재배치할 수 없다는 LinkedHashSet의 오랜 결함을 해결해준다.

### SequencedMap
* SequencedMap 역시 정해진 순서의 원소에 대한 공통 기능을 제공한다. SequenceSet에서와 마찬가지로 putFirst(K, V)와 putLast(K, V) 메소드는 원소가 이미 존재하는 경우에 적절한 위치로 재배치되는 특별한 의미를 갖는다. 이를 처리할 수 없는 SortedMap은 마찬가지로 UnsupportedOperationException을 던질 수 있다.

```JAVA
  interface SequencedMap<K,V> extends Map<K,V> {
    // new methods
    SequencedMap<K,V> reversed();
    SequencedSet<K> sequencedKeySet();
    SequencedCollection<V> sequencedValues();
    SequencedSet<Entry<K,V>> sequencedEntrySet();
    V putFirst(K, V);
    V putLast(K, V);
    // methods promoted from NavigableMap
    Entry<K, V> firstEntry();
    Entry<K, V> lastEntry();
    Entry<K, V> pollFirstEntry();
    Entry<K, V> pollLastEntry();
  }
```
### Collections
* 새로운 인터페이스가 추가됨에 따라 Collections 유틸에도 다음과 같은 기능이 추가될 예정이다.

```JAVA
Collections.unmodifiableSequencedCollection(sequencedCollection)
Collections.unmodifiableSequencedSet(sequencedSet)
Collections.unmodifiableSequencedMap(sequencedMap)
```

----
출처 : https://mangkyu.tistory.com/308 </br>
출처 : https://openjdk.org/jeps/431
