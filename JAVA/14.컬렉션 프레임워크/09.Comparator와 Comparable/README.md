## Comparable과 Comparator

- **TreeSet의 객체와 TreeMap의 키는 저장과 동시에 자동 오름차순으로 정렬**되는데,
    - 숫자(Integer, Double) 타입일 경우에는 값으로 정렬하고
    - 문자열(String) 타입일 경우에는 유니코드로 정렬한다.
- **TreeSet과 TreeMap은 정렬을 위해 `java.lang.Comparable`을 구현한 객체를 요구**하는데, Integer, Double, String은 모두 Comparable 인터페이스를 구현하고 있다.
- **사용자 정의 클래스도 Comparable을 구현한다면 자동 정렬이 가능하다.**
    - Comparable에는 **compareTo() 메소드**가 정의되어 있기 때문에 **사용자 정의 클래스**에서는 이 메소드를 **오버라이딩**하여 다음과 같이 리턴 값을 만들어 내야 한다.
    - 현재 객체의 숫자 - 비교대상 객체 숫자 : 오름차순
    - 비교 대상 객체 - 현재 객체 : 내림차순
        
   ![image](https://github.com/somi9954/Java/assets/137499604/35915b6f-a29a-4014-8087-3fee0b9cb456)

        
- Comparable: 기본 정렬기준을 구현하는데 사용 (Natrual Order)
- Comparator : 기본 정렬기준 외에 다른 기준으로 정렬하고자 할 때 사용 → Comparable 의 대안적인 기준

### ✅ 예제 | Comparable 구현 클래스

다음은 나이를 기준으로 Person 객체를 오름차순으로 정렬하기 위해 Comparable 인터페이스를 구현한 것이다.

나이가 적을 경우는 -1을, 동일한 경우는 0을, 클 경우는 1을 리턴하도록 compareTo() 메소드를 재정의하였다.

- Person

```java
public class Person implements Comparable<Person> {
    public String name;
    public int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public int compareTo(Person o) {
        if (age < o.age) return -1;
        else if (age == o.age) return 0;
        else return 1;
    }
}
```

- ComparableExample

```java
import java.util.Iterator;
import java.util.TreeSet;

public class ComparableExample {
    public static void main(String[] args) {
        TreeSet<Person> treeSet = new TreeSet<Person>();
        treeSet.add(new Person("김", 45));
        treeSet.add(new Person("이", 25));
        treeSet.add(new Person("최", 31));

        Iterator<Person> iterator = treeSet.iterator();
        while (iterator.hasNext()) {
            Person person = iterator.next();
            System.out.println(person.name + ": " + person.age);
        }
    }
}
```

### ✅ Comparable 비구현 객체 정렬

- **TreeSet의 객체와 TreeMap의 키가 Comparable을 구현하고 있지 않을 경우에는 저장하는 순간 ClassCastException이 발생한다.**
- **TreeSet 또는 TreeMap 생성자의 매개값으로 정렬자(Comparator)를 제공하면 Comparable 비구현 객체도 정렬시킬 수 있다.**

```java
TreeSet<E> treeSet = new TreeSet<E>( new AscendingComparator() );
TreeMap<K, V> treeMap = new TreeMap<K, V>( new DescendingComparator() );
```

정렬자는 **Comparator 인터페이스를 구현한 객체**를 말하는데, Comparator 인터페이스에는 다음과 같이 메소드가 정의되어 있다.

![image](https://github.com/somi9954/Java/assets/137499604/85387a3c-e258-46d5-9dff-816fda8e1259)

compare() 메소드는 비교하는 두 객체가 동등하면 0, 비교하는 값보다 앞에 오게 하려면 음수, 뒤에 오게 하려면 양수를 리턴하도록 구현하면 된다.

### ✅ 예제 | 내림차순 정렬자를 사용하는 TreeSet

다음은 가격을 기준으로 Fruit 객체를 내림차순으로 정렬시키는 정렬자이다.

- DescendingComparator

```java
import java.util.Comparator;

public class DescendingComparator implements Comparator<Fruit> {
    @Override
    public int compare(Fruit o1, Fruit o2) {
        if (o1.price < o2.price) return 1;
        else if (o1.price == o2.price) return 0;
        else return -1;
    }
}

```

- Fruit

```java
public class Fruit {
    public String name;
    public int price;

    public Fruit(String name, int price) {
        this.name = name;
        this.price = price;
    }
}
```

- ComparatorExample

```java
package book;

import java.util.Iterator;
import java.util.TreeSet;

public class ComparatorExample {
    public static void main(String[] args) {
        TreeSet<Fruit> treeSet = new TreeSet<Fruit>(new DescendingComparator());    //내림차순 정렬자 제공
        treeSet.add(new Fruit("포도", 3000));
        treeSet.add(new Fruit("수박", 10000));
        treeSet.add(new Fruit("딸기", 6000));

        Iterator<Fruit> iterator = treeSet.iterator();
        while (iterator.hasNext()) {
            Fruit fruit = iterator.next();
            System.out.println(fruit.name + ": " + fruit.price);
        }
    }
}
```

- 실행 결과

```java
수박: 10000
딸기: 6000
포도: 3000
```
