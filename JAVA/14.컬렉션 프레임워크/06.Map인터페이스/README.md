# Map 인터페이스(사전 자료구조)

- Map인터페이스는 키(key)와 값(value)을 하나의 쌍으로 묶어서 저장하는 컬렉션 클래스를 구현하는 데 사용된다.
- 키는 중복될 수 없지만 값은 중복을 허용한다.(집합 자료)
- 검색을 요구하는 데이터를 저장하는데는 효과적이지만, 데이터를 저장하고 삭제할 때는 다소 느린편이다.
- 만일 기존에 저장된 데이터와 중복된 키와 값을 저장하면 기존의 값은 없어지고 마지막에 저장된 값이 남게 된다.
- 저장 순서가 유지 되지 않는다
- 구현 클래스에는 HashMap,TreeMap, LinkedHashMap이 있다.

<img src="https://github.com/somi9954/Java/assets/137499604/be10dcaa-1eae-4b87-aa17-bd922f851b5c" width="500">

- Map 인터페이스의 메소드는 다음과 같다.

| 추상 메서드 | 설명 |
| --- | --- |
| void clear() | Map의 모든 객체를 삭제 |
| boolean containsKey(Object key) | 지정된 key객체와 일치하는 객체가 있는지 확인 |
| boolean containsValue(Object value) | 지정된 value객체와 일치하는 객체가 있는지 확인 |
| Set entrySet() | Map에 저장된 key-value쌍을 Map.Entry타입의 객체로저장한 Set을 반환 |
| boolean equals(Object o) | 동일한 Map인지 비교 |
| Object get(Object key) | 지정한 key객체에 대응하는 value객체를 반환 |
| int hashCode() | 해시코드를 반환 |
| boolean isEmpty() | Map이 비어있는지 확인 |
| Set keySet() | Map에 저장된 모든 key객체를 반환 |
| Object put(Object key, Object value) | Map에 key객체와 value객체를 연결(mapping)하여 저장 |
| void putAll(Map t) | 지정된 Map의 모든 key-value쌍을 추가 |
| Object remove(Object key) | 지정한 key객체와 일치하는 key-value객체를 삭제 |
| int size() | Map에 저장된 key-value쌍의 개수를 반환 |
| Collection values() | Map에 저장된 모든 value객체를 반환 |

<aside>
💡 Map 인터페이스의 메소드를 보면, Key값을 반환할때 Set 인터페이스 타입으로 반환하고, Value값을 반환할때 Collection 타입으로 반환하는걸 볼 수 있다.

Map 인터페이스에서 값(value)은 중복을 허용하기 때문에 Collection 타입으로 반환하고, 키(key)는 중복을 허용하지 않기 때문에 Set 타입으로 반환하는 것이다.

</aside>

## **Map.Entry 인터페이스**

- Map.Entry 인터페이스는 Map 인터페이스 안에 있는 내부 인터페이스이다.
- Map 에 저장되는 key - value 쌍의 Node 내부 클래스가 이를 구현하고 있다.
- Map 자료구조를 보다 객체지향적인 설계를 하도록 유도하기 위한 것이다.

<img src="https://github.com/somi9954/Java/assets/137499604/e9e254fc-fcf9-496a-9d19-cf7452dc07ff" width="400">

| 서드 | 설 명 |
| --- | --- |
| boolean equals(Object o) | 동일한 Entry 인지 비교 |
| Object getKey( ) | Entry 의 key 객체를 반환 |
| Object getValue( ) | Entry 의 value 객체를 반환 |
| int hashCode( ) | Entry 의 해시코드 반환 |
| Object setValue(Object value) | Entry 의 value 객체를 지정된 객체로 바꾼다. |

```java
Map<String, Integer> map = new HashMap<>();
map.put("a", 1);
map.put("b", 2);
map.put("c", 3);

// Map.Entry 인터페이스를 구현하고 있는 Key-Value 쌍을 가지고 있는 HashMap의 Node 객체들의 Set 집합을 반환
Set<Map.Entry<String, Integer>> entry = map.entrySet();

System.out.println(entry); // [1=a, 2=b, 3=c]

// Set을 순회하면서 Map.Entry를 구현한 Node 객체에서 key와 value를 얻어 출력
for (Map.Entry<String, Integer> e : entry) {
    System.out.printf("{ %s : %d }\n", e.getKey(), e.getValue());
```

<img src="https://github.com/somi9954/Java/assets/137499604/b39540e1-32c7-48fb-8064-a94934a27116" width="350">

## **HashMap 클래스**

- Hashtable을 보완한 컬렉션
- 배열과 연결이 결합된 Hashing형태로, 키(key)와 값(value)을 묶어 하나의 데이터로 저장한다
- 중복을 허용하지 않고 순서를 보장하지 않는다
- 키와 값으로 null이 허용된다
- 추가, 삭제, 검색, 접근성이 모두 뛰어나다
- HashMap은 비동기로 작동하기 때문에 멀티 쓰레드 환경에서는 어울리지않는다 (대신 ConcurrentHashMap 사용)
    
<img src="https://github.com/somi9954/Java/assets/137499604/69b667c8-d9e5-436a-a92e-472d154c833e" width="450">

```java
Map<String, String> hashMap = new HashMap<>();

hashMap.put("love", "사랑");
hashMap.put("apple", "사과");
hashMap.put("baby", "아기");

hashMap.get("apple"); // "사과"

// hashmap의 key값들을 set 집합으로 반환하고 순회
for(String key : hashMap.keySet()) {
    System.out.println(key + " => " + hashMap.get(key));
}
/*
love => 사랑
apple => 사과
baby => 아기
*/
```

### LinkedHashMap

<img src="https://github.com/somi9954/Java/assets/137499604/1572e009-c9b7-44fc-b652-0860da17ad5e" width="450">

- HashMap을 상속하기 때문에 흡사하지만, Entry들이 연결 리스트를 구성하여 데이터의 순서를 보장한다.
- 일반적으로 Map 자료구조는 순서를 가지지 않지만, LinkedHashMap은 들어온 순서대로 순서를 가진다.

```java
Map<Integer, String> hashMap = new HashMap<>();

hashMap.put(10000000, "one");
hashMap.put(20000000, "two");
hashMap.put(30000000, "tree");
hashMap.put(40000000, "four");
hashMap.put(50000000, "five");

for(Integer key : hashMap.keySet()) {
    System.out.println(key + " => " + hashMap.get(key)); // HashMap 정렬 안됨
}

// ----------------------------------------------

Map<Integer, String> linkedHashMap = new LinkedHashMap<>();

linkedHashMap.put(10000000, "one");
linkedHashMap.put(20000000, "two");
linkedHashMap.put(30000000, "tree");
linkedHashMap.put(40000000, "four");
linkedHashMap.put(50000000, "five");

for(Integer key : linkedHashMap.keySet()) {
    System.out.println(key + " => " + linkedHashMap.get(key)); // LinkedHashMap 정렬됨
}
```

<img src="https://github.com/somi9954/Java/assets/137499604/e9032126-22a9-405c-8c2a-16b758e6ea3b" width="350">

## ****Sorted Map****

- SortedMap은 key의 값이 Integer, Double 등과 같이 비교 가능한(Comparable) 타입이거나, SortedMap을 생성하는 시기에 별도의 Comparator를 등록해서 정렬할 수 있습니다.
- Map 인터페이스를 상속한다. 구현하는 클래스는 Map인터페이스에서 제공하는 메소드도 모두 구현해야 한다.
- 메소드는 다음과 같다.
1. **Comparator comparator()** 

SortedMap에 등록된 Comparator가 있으면 해당 인스턴스를 리턴하고, 별도로 등록된게 없으면 null을 리턴합니다.

1. **K firstKey()**

첫번째 Key를 리턴합니다. 오름차순의 경우 가장 작은 값(lowest)을 리턴합니다.

1. **K lastKey()**

마지막 Key를 리턴합니다. 오름차순의 경우 가장 큰 값(highest)을 리턴합니다.

1. **SortedMap headMap(K toKey)**

인자로 받은 toKey 보다 작은 Key들을 가지고서 부분적인 Map을 리턴합니다.

1. **sortedMap tailMap(K fromKey)**

인자로 받은 fromKey 보다 큰 Key들을 가지고서 부분적인 Map을 리턴합니다.

- 대표적인 구현 클래스는 TreeMap이다.

### TreeMap

- 이진 검색 트리의 형태로 키와 값의 쌍으로 이루어진 데이터를 저장 (TreeSet 과 같은 원리)
- TreeMap은 SortedMap 인터페이스를 구현하고 있어 Key 값을 기준으로 정렬되는 특징을 가지고 있다.
- 정렬된 순서로 키/값 쌍을 저장하므로 빠른 검색(특히 범위 검색)이 가능하다
- 단, 키와 값을 저장하는 동시에 정렬을 행하기 때문에 저장시간이 다소 오래 걸리다
- 정렬되는 순서는 숫자 → 알파벳 대문자 → 알파벳 소문자 → 한글 순이다.
- TreeSet과는 달리 키와 값이 저장된 Map.Entry를 저장한다.

> TreeMap을 생성하기 위해서는 키로 저장할 객체 타입과 값으로 저장할 객체 타입을 타입 파라미터로 주고 기본 생성자를 호출하면 된다.
> 
> 
> ```java
> TreeMap<K, V> treeMap = new TreeMap<K, V>();
> ```
> 
- 키로 String 타입을 사용하고 값으로 Integer 타입을 사용하는 TreeMap은 다음과 같이 생성할 수 있다.

```java
TreeMap<String, Integer> treeMap = new TreeMap<String, Integer>();
```

Map 인터페이스 타입 변수에 대입해도 되지만  TreeMap클래스 타입으로 대입한 이유는 특정 객체를 찾거나 범위 검색과 관련된 메소드를 사용하기 위해서이다.

- TreeMap 메소드는 다음과 같다.

![image](https://github.com/somi9954/Java/assets/137499604/7bc4e2e1-4a2e-413b-bb0e-bb702b3d9ced)

![image](https://github.com/somi9954/Java/assets/137499604/8d0d895f-8f53-46d9-9baa-2b1c201b3e8f)


- descendingKeySet() 메소드는 내림차순으로 정렬된 NavigableSet 객체를 리턴한다.
- descendingMap() 메소드는 내림차순으로 정렬된 NavigableMap 객체를 리턴한다.
NavigableMap은 firstEntry(), lastEntry(), lowerEntry(), higherEntry(), floorEntry(), ceilingEntry() 메소드를 제공하고, 오름차순과 내림차순으로 번갈하며 정렬 순서를 바꾸는 descendingMap() 메소드도 제공한다.
- 오름차순으로 정렬하고 싶다면 다음과 같이 descendingMap() 메소드를 두 번 호출하면 된다.

```java
NavigableMap<K, V> descendingMap = treeMap.descendingMap();
NavigableMap<K, V> ascendingMap = descendingMap.descendingMap();
```

<img src="https://github.com/somi9954/Java/assets/137499604/d9046e37-9fad-4ba0-b723-babb5fb0d59a">

- 세 가지 메소드 중에서 subMap() 메소드의 사용 방법을 자세히 살펴보도록 하자. subMap() 메소드는 네 개의 매개 변수가 있는데, 시작 키와 끝 키, 그리고 이 키들의 Map.Entry를 포함할지 여부의 boolean 값을 받는다.

```java
NavigableMap<K, V> subMap = treeMap.subMap(K fromKey, boolean fromInclusive, K toKey, boolean toInclusive);
```

K fromKey: 시작 키
boolean fromInclusive: 시작 Map.Entry 포함 여부
K toKey: 끝 키
boolean toInclusive: 끝 Map.Entry 포함 여부

```java
import java.util.Map;
import java.util.TreeMap;

public class TreeMapExample {
    public static void main(String[] args) {
        TreeMap<Integer, String> scores = new TreeMap<Integer, String>();
        scores.put(87, "김");
        scores.put(98, "이");
        scores.put(75, "박");
        scores.put(95, "최");
        scores.put(80, "윤");

        Map.Entry<Integer, String> entry = null;

        entry = scores.firstEntry();
        System.out.println("가장 낮은 점수: " + entry.getKey() + "-" + entry.getValue());

        entry = scores.lastEntry();
        System.out.println("가장 높은 점수: " + entry.getKey() + "-" + entry.getValue() + "\n");

        entry = scores.lowerEntry(95);
        System.out.println("95점 아래 점수: " + entry.getKey() + "-" + entry.getValue());

        entry = scores.higherEntry(95);
        System.out.println("95점 위의 점수: " + entry.getKey() + "-" + entry.getValue() + "\n");

        entry = scores.ceilingEntry(95);
        System.out.println("95점 이거나 바로 아래 점수: " + entry.getKey() + "-" + entry.getValue());

        entry = scores.floorEntry(95);
        System.out.println("95점 이거나 바로 위의 점수: " + entry.getKey() + "-" + entry.getValue() + "\n");

        while (!scores.isEmpty()) {
            entry = scores.pollFirstEntry();
            System.out.println(entry.getKey() + "-" + entry.getValue() + " (남은 객체 수: " + scores.size() + ")");
        }

    }
}
```

<img src="https://github.com/somi9954/Java/assets/137499604/952b67c2-c2d9-4956-a356-dfd4d21ef496" width="350">

## Hashtable

- HashMap과 동일한 내부 구조를 가지고 있습니다.
- Key를 특정 해시 함수를 통해 해싱한 후 나온 결과를 배열의 인덱스로 사용하여 Value를 찾는 방식으로 동작된다.
- 키와 값으로 null이 허용 하지 않는다.
- HashMap과 가장 큰 차이점은 동기화된 메소드로 구성되어 있기 때문에 멀티 스레드가 동시에

이 메소드를 사용할 수 없고 하나의 스레드가 종료되면 다른 스레드를 실행할 수 있습니다.

- 그래서 멀티 스레드 환경에서 안전하게 객체를 추가, 삭제할 수 있습니다.(스레드 안전)

사용하는 방법은 HashMap과 동일합니다.

```java
package Collection;
 
import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.Reader;
import java.util.Hashtable;
import java.util.Map;
 
public class MapCollection {
 
    public static void main(String[] args) throws IOException {
 
        Map<String, String> hashTable = new Hashtable<String, String>();
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        String id,pw;
        
        hashTable.put("Jimmy", "1234");
        hashTable.put("Rain", "2345");
        hashTable.put("Nick", "3456");
        hashTable.put("Josh", "4567"); // 현재 테이블에 저장된 아이디 비밀번호
        
        while(true) {
            System.out.println("아이디와 비밀번호를 입력하세요");
            System.out.print("아이디 : ");
            id = br.readLine(); // 입력받는 곳
            
            System.out.print("비밀번호 : ");
            pw = br.readLine(); // 입력받는 곳
            
            if(hashTable.containsKey(id)) { // id와 같은 key가 있으면 true
                if(hashTable.get(id).equals(pw)) { // pw 체크
                    System.out.println("로그인에 성공하였습니다.");
                    break;
                } else {
                    System.out.println("비밀번호가 다릅니다.");
                }
            } else {
                System.out.println("존재하지 않는 아이디입니다.");
            }
        }
    }
} // containsKey( ) 메소드는 테이블 안에 매개변수로 들어온 값과 일치하는 것이 있는지 
  // 찾아줍니다. 있으면 true 없으면 false를 반환합니다.
```

<img src="https://github.com/somi9954/Java/assets/137499604/3abdfdfb-7f64-457d-9a9b-10760aa8d53d" width="350">

### **Properties**

- Properties는 Hashtable의 하위 클래스 이기 때문에 Hashtable 의 특징을 모두 가지고 있습니다.
- 가장 큰 특징은 키와 값을 오직 String 타입으로 밖에 사용 못합니다.
- 그래서 주로 애플리케이션의 옵션 정보, 데이터 베이스 연결 정보, 다국어 정보의 파일을 읽을 때

사용합니다.

```java
public class PropertiesEx1 {
    public static void main(String[] args) {
        Properties properties = new Properties();

        properties.setProperty("timeout", "30");
        properties.setProperty("language", "kr");
        properties.setProperty("size", "10");
        properties.setProperty("capacity", "10");

        // properties에 저장된 요소들을 Enumeration을 이용해 출력
        Enumeration enumeration = properties.propertyNames();

        while (enumeration.hasMoreElements()) {
            String element = (String) enumeration.nextElement();
            System.out.println(element + "=" + properties.getProperty(element));
        }

        System.out.println();

        properties.setProperty("size", "20");
        System.out.println("size=" + properties.getProperty("size"));
        System.out.println("capacity=" + properties.getProperty("capacity", "20"));
        System.out.println("loadfactor=" + properties.getProperty("loadfactor", "0.75"));

        System.out.println(properties);

        System.out.println();

        properties.list(System.out);
    }
}
```

<img src="https://github.com/somi9954/Java/assets/137499604/9961090b-f9ea-4657-8341-588424f31b1e" width="350">

- properties의 기본적인 메서드를 이용해서 저장하고, 읽어오고, 출력하는 방법을 보여주는 예제이다.
- 데이터를 저장하는데 사용되는 setProperty()는 단순히 Hashtable의 put메서드를 호출한다.
- setProperty()는 기존에 같은 키로 저장된 값이 있는 경우 그 값을 Object타입으로 반환하며, 그렇지 않을 경우 null을 반환한다.
- getProperty()는 properties에 저장된 값을 읽어오는 일을 하는데 만일 읽어오려는 키가 존재하지 않으면 지정된 기본값을 반환한다.
- Properties는 컬렉션프레임워크 이전의 구버전이기 때문에 Iterator가 아닌 Enumeration을 사용한다.
- list()를 이용하면 Properties에 저장된 모든 데이터를 화면 또는 파일에 편리하게 출력할 수 있다.

### ⭐정리
```java
추가

put(K k , V v)

putifAbsent(K k, V v) : k가 없을때만 v값을 추가

수정

put(K k , V v)

replace(K k , V v)

replace(K k, V old, V new)

삭제

remove(Object k)

조회

 V get(Object k) 

V getOrDefault(Object, k , V v)

Set<K> keySet(): 전체 키 값

Collection<V> values() : 전체 값

boolean containsKey(Object k)

boolean containsValue(Object v)

기타

int size() : 요소 갯수
```
