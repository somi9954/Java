# StringBuffer와 Stringbuilder 클래스

자바에서 문자열을 처리하는 변수는 String 객체이다. String 클래스는 최초 지정된 문자열 이후에 값이 추가되면 내부적으로 새로운 메모리를 할당해 새로운 문자열을 등록한다

![image](https://github.com/somi9954/Java/assets/137499604/3f422da8-7d6b-40aa-8668-b5b03a12c9bb)


위의 그림처럼 처음 문자열을 선언한 후 추가하면 기존의 메모리 주소가 아닌 새로운 주소에 추가된 문자가 저장된다. 따라서 문자열을 많이 사용할수록 메모리 사용이 늘어나 메모리가 낭비가 될 수 있다.

이런 문제점을 해결하기 위해 가변 속성을 지닌 StringBuffer 또는 Stringbuilder 클래스를 사용한다.

StringBuffer와 StringBuilder는 내부에 여유 공간을 두기 때문에 문자열을 합칠 때 메모리에 생성하는 과정을 String 보다 현저히 생략할 수 있다. 

# StringBuffer

- String 클래스는 인스턴스를 생성할 때 지정된 문자열을 변경할 수 없지만 StringBuffer클래스는 변경이 가능하다. 내부적으로 문자열 편집을 위한 버퍼(buffer)를 가지고 있으며, StringBuffer인스턴스를 생성할 때 그 크기를 지정할 수 있다.
- 기본적으로 StringBuffer의 버퍼(데이터 공간)의 크기의 기본값은 16개의 문자를 저장할 수 있는 크기이다.
- 편집할 문자열의 길이를 고려하여 버퍼의 길이를 충분히 잡아주는 것이 좋다. 편집중인 문자열이 버퍼의 길이를 넘어서게 되면 버퍼의 길이를 늘려주는 작업이 추가로 수행되어야 하기 때문에 작업 효율이 떨어진다.
- **내부에 변경가능한 ( final이 아닌) char[](JDK12에서 byte[]로 변경)를 변수**로 가지고 있다.
- 클래스를 사용하여 문자열을 연결하면 기존에 사용하던 char[] 배열이 확장되므로 추가 메모리를 사용하지 않는다.
- tringBuffer 클래스는 문자열이 안전하게 변경되도록 보장된다.
- 쓰레드 환경에서 안정성 기능을 추가로 가진다. 왜냐하면 내부 메서드 별로 synchronized(동기화) 키워드가 선언되기 때문입니다.

> String buffers are safe for use by multiple threads. The methods are synchronized where necessary so that all the operations on any particular instance behave as if they occur in some serial order that is consistent with the order of the method calls made by each of the individual threads involved.   (문자열 버퍼는 여러 스레드에서 사용해도 안전합니다. 메서드는 필요한 경우 동기화되어 특정 인스턴스에 대한 모든 작업이 관련된 개별 스레드에서 수행된 메서드 호출의 순서와 일치하는 일련의 순서로 발생하는 것처럼 작동합니다.)
> 

<aside>
💡 참고)

**Synchronized(동기화)란?**

- 공유 데이터에 lock을 걸어 작업중이던 쓰레드가 마칠때까지 다른 쓰레드에게 제어권이 넘어가지 않게 보호한다.

- Synchronized 블럭이 끝나면 lock이 풀리고 다른 쓰레드도 접근 가능하게 된다.

- 교착상태(dead-lock)이 빠질 위험이 있으므로 주의한다.

자세한 내용은 쓰레드에서 정리한다.

</aside>

### **StringBuffer 내장 메소드**

<table>
  <tr>
    <th>메서드</th>
    <th>설명</th>
  </tr>
  <tr>
    <td>StringBuffer( )</td>
    <td>버퍼의 길이를 지정하지 않으면 크기가  16인 버퍼를 생성</td>
  </tr>
  <tr>
    <td>StringBuffer(int length)</td>
    <td>length 길이를 가진  StringBuffer 클래스의 인스턴스(buffer)를 생성</td>
  </tr>
  <tr>
    <td>StringBuffer(String str)</td>
    <td>지정한 문자열( str )의 길이보다  16 만큼 더 큰 버퍼를 생성</td>
  </tr>
  <tr>
    <td>
      StringBuffer append(boolean b)<br>
      StringBuffer append(char c) <br>
      StringBuffer append(char[] str)<br>
      StringBuffer append(double d) <br>
      StringBuffer append(float f) <br>
      StringBuffer append(int i) <br>
      StringBuffer append(long l) <br>
      StringBuffer append(Object obj) <br>
      StringBuffer append(String str) <br>
    </td>
    <td>매개변수로 입력된 값을 문자열로 변환하여  StringBuffer 인스턴스가 저장하고 있는 문자열의 뒤에 덧붙임</td>
  </tr>
  <tr>
    <td> int capacity( )</td>
    <td>StringBuffer 인스턴스의 버퍼크기 반환 (자료형의 할당된 크기를 반환)</td>
  </tr>
    <tr>
    <td>int length( )</td>
    <td>StringBuffer 인스턴스에 저장된 문자열의 길이 반환 (버퍼에 담긴 문자열 데이터를 반환)</td>
  </tr>
     <tr>
    <td>char charAt(int index)</td>
    <td>지정된 위치( index )에 있는 문자를 반환</td>
  </tr>
    <tr>
    <td>StringBuffer delete(int start, int end)</td>
    <td>시작위치( start )부터 끝 위치( end )사이에 있는 문자를 제거단,  end 위치의 문자는 제외(start <= x < end) </td>
  </tr>
    <tr>
    <td>StringBuffer deleteCharAt(int index)</td>
    <td>지정된 위치( index )의 문자를 제거</td>
  </tr>
  <tr>
    <td>
      StringBuffer insert(int pos, boolean b)<br>
      StringBuffer insert(int pos, char c)<br>
      StringBuffer insert(int pos, char[ ] str)<br>
      StringBuffer insert(int pos, doule d)<br>
      StringBuffer insert(int pos, float f)<br>
      StringBuffer insert(int pos, int i)<br>
      StringBuffer insert(int pos, long l)<br>
      StringBuffer insert(int pos, Object obj)<br>
      StringBuffer insert(int pos, String str) <br>
    </td>
    <td>두 번째 매개변수로 받은 값을 문자열로 변환하여 지정된 위치( pos )에 추가( pos 는 0부터 시작)</td>
  </tr>
    <tr>
    <td>StringBuffer replace(int start, int end, String str)</td>
    <td>지정된 범위( start  ~  end )의 문자들을 주어진 문자열로 바꾼다.단,  end 의 위치는 범위에 포함되지 X (start <= x < end)</td>
  </tr>
    <tr>
    <td>StringBuffer reverse( )</td>
    <td>StringBuffer 인스턴스에 저장되어 있는 문자열의 순서를 거꾸로 나열</td>
  </tr>
    <tr>
    <td>void setCharAt(int index, char ch)</td>
    <td>지정된 위치( index )의 문자를 주어진 문자( ch )로 바꾼다.</td>
  </tr>
    <tr>
    <td>void setLength(int newLength)</td>
    <td>지정된 길이로 문자열의 길이를 변경길이를 늘리는 경우에는 나머지 빈공간들을 널문자( \u0000 )로 채운다.</td>
  </tr>
    <tr>
    <td>String toString( )</td>
    <td>StringBuffer 인스턴스의 문자열을  String 으로 변환</td>
  </tr>
    <tr>
    <td>String substring(int start)<br>
      String substring(int start, int end)<br>
    </td>
    <td>
      시작위치에서 끝까지 문자열 리턴<br>
      시작위치에서 끝 사이의 문자열 리턴
    </td>
  </tr>
</table>
      
```java
package exam06;

public class ex01 {
    public static void main(String[] args) {

    String str = "abcdefg";
    StringBuffer sb = new StringBuffer(str); // String -> StringBuffer

    System.out.println("처음 상태 : " + sb); // 처음상태 : abcdefg

    System.out.println("문자열 String 변환 : " + sb.toString()); // StringBuffer를 String으로 변환하기

    System.out.println("문자열 추출 : " + sb.substring(2,4)); // 문자열 추출하기

    System.out.println("문자열 추가 : " + sb.insert(2,"추가")); // 문자열 추가하기

    System.out.println("문자열 삭제 : " + sb.delete(2,4)); // 문자열 삭제하기

    System.out.println("문자열 연결 : " + sb.append("hijk")); // 문자열 붙이기

    System.out.println("문자열의 길이 : " + sb.length()); // 문자열의 길이구하기

    System.out.println("용량의 크기 : " + sb.capacity()); // 용량의 크기 구하기

    System.out.println("문자열 역순 변경 : " + sb.reverse()); // 문자열 뒤집기

    System.out.println("마지막 상태 : " + sb); // 마지막상태 : kjihgfedcba
    }
}
```

![image](https://github.com/somi9954/Java/assets/137499604/89a001d2-6fcc-41ca-9cf3-ab8c8db49252)


# StringBuilder

- **내부에 변경가능한 ( final이 아닌) char[](JDK12에서 byte[]로 변경)를 변수**로 가지고 있다.
- 클래스를 사용하여 문자열을 연결하면 기존에 사용하던 char[] 배열이 확장되므로 추가 메모리를 사용하지 않는다.
- 쓰레드 환경이 아닌 경우에는 StringBuilder의 성능이 좋아지므로 일반적인 프로그래밍에서는 StringBuilder의 사용을 권장한다.
- StringBuilder 의 메서드는 StringBuffer와 동일하다.

| 메서드명 | 설명 |
| --- | --- |
| append(String str) | 기존 문자열 뒤에 더하여 반환 |
| delete(int start, int end) | 시작 위치부터 끝 위치 전까지 삭제 |
| insert(int offset, String str) | 시작 위치부터 문자열을 삽입 |
| reverse() | 문자열을 반대로 출력  |

```java
package exam01;

import java.io.IOException;

public class ex02 {
    public static void main(String[] args) throws IOException {
        StringBuilder sb = new StringBuilder("aaa");

        // 문자열 추가
        System.out.println(sb.append("bbb")); // aaabbb
        System.out.println(sb.append(4)); // aaabbb4

        // 문자열 삽입
        System.out.println(sb.insert(2, "ccc")); // aacccabbb4

        // 문자열 치환, 문자열 교체
        System.out.println(sb.replace(3, 6, "ye")); // aacyebbb4

        // 인덱싱, 문자열 자르기
        System.out.println(sb.substring(5)); // bbb4
        System.out.println(sb.substring(3, 7)); // yebb

        // 문자 삭제
        System.out.println(sb.deleteCharAt(3)); // aacebbb4

        // 문자열 삭제
        System.out.println(sb.delete(3, sb.length())); // aac

        // 문자열 변환
        System.out.println(sb.toString()); // aac

        // 문자열 뒤집기
        System.out.println(sb.reverse()); // caa

        // 문자 대체, 문자 교체, 문자 치환
        sb.setCharAt(1, 'b');
        System.out.println(sb); // cba

        // 문자열 길이 조정
        sb.setLength(2);
        System.out.println(sb); // cb
    }
}
```

![image](https://github.com/somi9954/Java/assets/137499604/c8c27625-e074-4a50-9bf5-ff9cef5a5258)


# 문자열 자료형 비교 총정리

| String | StringBuffer | StringBuilder |
| --- | --- | --- |
| 가변 여부 | 불변 | 가변 |
| 스레드 세이프 | O | O |
| 연산 속도 | 느림 | 빠름 |
| 사용 시점 | 문자열 추가 연산이 적고, 스레드 세이프 환경에서 | 문자열 추가 연산이 많고, 스레드 세이프 환경에서 |
- **String 을 사용해야 할 때 :**
    - String은 불변성
    - 문자열 연산이 적고 변하지 않는 문자열을 자주 사용할 경우
    - 멀티쓰레드 환경일 경우
- **StringBuilder 를 사용 해야 할 때 :**
    - StringBuilder는 가변성
    - 문자열의 추가, 수정, 삭제 등이 빈번히 발생하는 경우
    - 동기화를 지원하지 않아, 단일 쓰레드이거나 동기화를 고려하지 않아도 되는 경우
    - 속도면에선 StringBuffer 보다 성능이 좋다.
- **StringBuffer 를 사용해야 할 때 :**
    - StringBuffer는 가변성
    - 문자열의 추가, 수정, 삭제 등이 빈번히 발생하는 경우
    - 동기화를 지원하여, 멀티 스레드 환경에서도 안전하게 동작
