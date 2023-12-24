## 정규식(Regular Expression) - java.util.regex패키지

- 정규식이란 텍스트 데이터 중에서 원하는 조건(패턴, pattern)과 일치하는 문자열을 찾아 내기 위해 사용하는 것으로 미리 정의된 기호와 문자를 이용해서 작성한 문자열을 말한다.
- 원래 Unix에서 사용하던 것이고 Perl의 강력한 기능이었는데, 요즘은 Java를 비롯해 다양한 언어에서 지원하고 있다.
- 정규식을 이용하면 많은 양의 텍스트 파일 중에서 원하는 데이터를 손쉽게 뽑아낼 수도 있고 입력된 데이터가 형식에 맞는지 체크할 수 도 있다. 예를 들면 html문서에서 전화번호나 이메일 주소만을 바로 추출한다던가, 입력한 비밀번호가 숫자와 영문자의 조합으로 되어 있는지 확인할 수도 있다.
- Pattern과 Matcher클래스를 주로 사용한다.
- Pattern 클래스의 메소드 중  compile, matcher 많이 사용한다
- Matcher 클래스의 메소드 중  find , group 많이 사용한다.

![image](https://github.com/somi9954/Java/assets/137499604/008106e5-fe38-4bd3-8af4-5e2492d399f0)


### 정규표현식 패턴

- 정규   표현식은   표준인   POSIX 의   정규    표현식과   POSIX  정규   표현식에서   확장된
Perl 방식의   PCRE 가   대표적이며, 이외에도    수많은    정규표현식이    존재하며    정규   표현식 간에는   약간의   차이점이   있으나   거의   비슷합니다. 정규   표현식에서    사용하는    기호를
Meta 문자라고    합니다. Meta 문자는    표현식    내부에서    특정한   의미를   갖는   문자를 말한다.
- POSIX 에서만   사용하는   문자클래스가    있는데, 단축키처럼    편리하게   사용할    수   있습니다. 대표적인   POSIX  문자클래스는    다음과   같으며   대괄호'[ ]'  가   붙어있는   모양   자체가표현식이므로   실제로   문자클래스로    사용할    때에는    대괄호를    씌워서    사용해야만   정상적인 결과를   얻을    수   있습니다.
- 이밖에도   [:cntrl:] :  아스키    제어문자(0~31 번, 127 번), [:print:] :  출력    가능한    모든   문자, [:xdigit:] :  모든   16 진수   숫자    등이   있습니다.

| 정규식 패턴 | 설명 |
| --- | --- |
| abc | 문자열을 포함한다 |
| [abc] | 문자클래스 - 문자집합안에 특정 문자 한개 |
| [^abc] | 부정문자클래스 : 문자 집합안의 특정 문자 한개 |
| [a-z] | 두 문자 사이의 모든 문자 |
| [^a-z] | 소문자 알파벳을 제외한 문자  |
| [^0-9] | 숫자가 아닌 문자가 포함된 패턴 == \D  |
| [0-9] | 숫자가 포함 되어 있는지 확인 <br> 모든 숫자 [0-9]와 같음 == \d |
| . | 줄 바꿈 문자를 제외한 문자 한개 (줄 개행 문자(\n)를 포함하지 않는) |
| \d | 모든 숫자[0-9]와 같음 |
| \D | 숫자를 제외한 모든 문자 한개 [^0-9]와 같음 |
| \w | 임의의 영어 단어 문자(알파벳, 숫자, 언더스코어) 한개 [a-zA-Z0-9_] |
| \W | 영어단어 문자(알파벳, 숫자, 언더스코어)를 제외한 문자 한개 |
| \s | 모든 공백 문자 한 개 |
| \S | 공백문자가 아닌 문자 한개 |
| \b | 단어의 경계 |
| x{2,4} | x를 최소 2번, 최대 4번 반복 |
| x{2,} | x를 2번 이상  반복 |
| x? | x를 한번 이하 반복 있어도 되고 없어도 되는 패턴 ⇒ 패턴 {0,1}  |
| x+ | x를 한번 이상 반복 ⇒ 패턴 {1, }  즉, 최대한의 매칭 |
| x* | x를 0번 이상 반복 ⇒ 패턴 {0,  } ⇒ 즉, 최소한의 매칭 |
| (x) | x를 그룹화(부분 정규 표현식 → 부분 패턴의 문자열 추출 ) <br> ex ) 이미지 경로 src 주소 추출하기  |
| ^ | 문자열의 시작 위치 <br> 참고) 문자 클래스 패턴 [^...] -> 제외한 문자 |
| $ | 문자열의 마지막 위치 |
| x &#124; y &#124; z | x,y,z 중 하나(선택) |

![image](https://github.com/somi9954/Java/assets/137499604/1f549dc4-3825-48d3-9c74-27e982cf03dd)

## 자주 쓰이는 정규식 패턴

| 분류 | 정규식 패턴 |
| --- | --- |
| 숫자 | ^[0-9]*$ |
| 영문자 | ^[a-zA-Z]*$ |
| 한글 | ^[가-힣]*$ |
| 영어&숫자 | ^[a-zA-Z0-9]*$ |
| 비밀번호 (숫자, 문자 포함의 6~12자리 이내) | ^[A-Za-z0-9]{6,12}$ |
| 비밀번호 (숫자, 문자, 특수문자 포함 8~15자리 이내) | ^.*(?=^.{8,15}$)(?=.*\d)(?=.*[a-zA-Z])(?=.*[!@#$%^&+=]).*$ |
| 이메일 | ^[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_.]?[0-9a-zA-Z])*.[a-zA-Z]{2,3}$ |
| 휴대전화 | ^\\d{3}-\\d{3,4}-\\d{4}$ |
| 일반전화 | ^\\d{2,3}-\\d{3,4}-\\d{4}$ |
| 주민등록번호 | \d{6} \- [1-4]\d{6} |
| 파일확장자 | ^\\S+.(?i)(txt|pdf|hwp|xls)$ |
| 이중 파일확장자 | (.+?)((\\.tar)?\\.gz)$ |

day11/utils/RegularEx1.java

```java
package day11.utils;

import java.util.regex.*;

public class RegularEx1 {
	public static void main(String[] args) {
		String[] data = {"bat", "baby", "bonus", "cA", "ca", "co", "c.", "c0", "car", "combat", "date", "disc"};
		Pattern p = Pattern.compile("c[a-z]*");

		for (int i = 0; i < data.length; i++) {
			Matcher m = p.matcher(data[i]);
			if (m.matches()) {
				System.out.print(data[i] + ",");
			}
		}
	}
}

실행결과

ca,co,car,combat,

```

1. 정규식을 매개변수로 Pattern클래스의 static 메서드인 Pattern compile(String regex)을 호출하여 Pattern인스턴스를 얻는다.

```java
Pattern p = Pattern.compile("c[a-z]*");

```

1. 정규식으로 비교할 대상을 매개변수로 Pattern클래스의 Matcher matcher(CharSequence input)를 호출해서 Matcher인스턴스를 얻는다.

```java
Matcher m = p.matcher(data[i]);

```

1. Matcher인스턴스에 boolean matches()를 호출해서 정규식에 부합하는지 확인한다.

```java
if (m.matches()) {
	...
}

```

> CharSequence는 인터페이스로 이를 구현한 클래스는 CharBuffer, String, StringBuffer가 있다.
> 

day11/utils/RegularEx2.java

```java
`package day11.utils;

import java.util.regex.*;

public class RegularEx2 {
	public static void main(String[] args) {
		String source = "HP:011-1111-1111, HOME:02-999-9999 ";
		String pattern = "(0\\d{1,2})-(\\d{3,4})-(\\d{4})";
		
		Pattern p = Pattern.compile(pattern);
		Matcher m = p.matcher(source);
		
		int i = 0; 
		while(m.find()) {
			System.out.println(++i + ": " + m.group() + " -> " + m.group(1) + ", " + m.group(2) + ", " + m.group(3));
		}
	}
}

실행결과

1: 011-1111-1111 -> 011, 1111, 1111
2: 02-999-9999 -> 02, 999, 9999`
```

**example**

```java
package exam01;

import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Ex01 {
    public static void main(String[] args) {
        // Pattern pattern = Pattern.compile("abc"); //abc 문자열이 포함 되어 있는지 확인 하는 패턴
        //Pattern pattern = Pattern.compile("[a-zA-z]"); //b 아니면 d가 하나라도 포함 되어 있는지 확인
        //Pattern pattern = Pattern.compile("[a-z]", Pattern.CASE_INSENSITIVE);
        //Pattern pattern = Pattern.compile("[0-9]");
        //Pattern pattern = Pattern.compile("\\d"); \ -> 역슬래시
        // Pattern pattern = Pattern.compile("[^a-zA-z]");
        //Pattern pattern = Pattern.compile("[^a-z]", Pattern.CASE_INSENSITIVE);
        //Pattern pattern = Pattern.compile("[^0-9]");
        Pattern pattern = Pattern.compile("\\D");
        String[] strs = { "AB", "abcd", "bcd", "efg", "1234", "!@#$%^"};
        for (String str: strs) {
            Matcher matcher = pattern.matcher(str);
            if (matcher.find()) {
                System.out.println(str);
            }
        }
    }
}
```

**공백문자 쪼개기** 

- 보통은 String 클래스의 split를 사용한다.

```java
package exam01;

import java.util.Arrays;

public class Ex02 {
    public static void main(String[] args) {
        String fruits = "Apple  Melon Mango   Banana";
        String[] fruits2 = fruits.split(" ");
        System.out.println(Arrays.toString(fruits2));
    }
}
```

- 하지만 결과값이 아래와 같이 나온다. (한계점 : 공백이 일정하지 않을 경우)

![image](https://github.com/somi9954/Java/assets/137499604/1f06854b-fc45-4156-80c7-7bcfefc5ee1e)


- 그래서 정규표현식을 사용하여 사용한다.

```java
import java.util.Arrays;

public class Ex02 {
    public static void main(String[] args) {
        String fruits = "Apple  Melon Mango   Banana";
        String[] fruits2 = fruits.split("\\s+");
        System.out.println(Arrays.toString(fruits2));
    }
}
```

- 아래와 같이 동일한 결과 값이 나온다

![image](https://github.com/somi9954/Java/assets/137499604/aba8a471-bd57-4374-a25c-ab538d39abe7)


**정규표현식 패턴으로 휴대폰 번호 형식 가져오기** 

- 간단하게 사용시 **[matches](https://www.notion.so/Regular-Expression-javautile-regex-7fc2dff3f7aa4410a13e08dd514251e5?pvs=21)**(**[String](https://www.notion.so/somicho92/String.html)** regex) 사용한다.

```java
package exam01;

import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Ex04 {
    public static void main(String[] args) {
        String[] mobiles =  {
                "032-320-1234",
                "016-210-1234",
                "010-1234-1234",
                "011-123-123"
        };
        Pattern pattern = Pattern.compile("01[016]-\\d{3,4}-\\d{4}");
        for (String mobile: mobiles) {
            Matcher matcher = pattern.matcher(mobile);
            if (matcher.find()) {
                System.out.println(mobile);
            }
        }
    }
}
```

- 빨간색으로 010 체크, 회색으로 011 체크, 핑크색으로 016 체크하여 패턴이 있는지 확인한다.
    
   ![image](https://github.com/somi9954/Java/assets/137499604/16957654-5c09-4626-944b-66125dcb07eb)

- 원하는 패턴을 주면 원하는 값이 나오게 된다.

```java
        Pattern pattern = Pattern.compile("01[016]-\\d{3,4}-\\d{4}");
        for (String mobile: mobiles) {
            Matcher matcher = pattern.matcher(mobile);
            if (matcher.find()) {
                System.out.println(mobile);
            }
```

![image](https://github.com/somi9954/Java/assets/137499604/efd4b5b7-1c6d-4f50-92ba-92e7a87998a3)

- 하지만 `"000010-1234-12340000"` 를 추가해도 결과값에 표기가 된다 그래서 앞에 ^을 표현하여 결과값을 원하는 010,011,016만 나올 수 있게 입력하여야 한다.
- `"010-1234-12340000"` 를 입력하여도 결과값이 출력이 된다.  끝나는 쪽에 $을 표현하여 결과값을 원하는 값으로 나올 수 있게 된다.

```java
package exam01;

import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Ex04 {
    public static void main(String[] args) {
        String[] mobiles =  {
                "032-320-1234",
                "016-210-1234",
                "010-1234-1234",
                "011-123-123",
                "000010-1234-12340000",
                "010-1234-12340000"
        };
        Pattern pattern = Pattern.compile("^01[016]-\\d{3,4}-\\d{4}$");
        for (String mobile: mobiles) {
            Matcher matcher = pattern.matcher(mobile);
            if (matcher.find()) {
                System.out.println(mobile);
            }
        }
    }
}
```

![image](https://github.com/somi9954/Java/assets/137499604/e8c5fae2-6f20-477f-b163-b516f3080510)

**example2**

```jsx
package exam01;

import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class Ex08 {
    public static void main(String[] args) {
        String[] persons = {
                "이이름 : 010-1234-1234",
                "김이름     :010-1234-1234",
                "박이름: 010-1000-1000"
        };

        String pattern = "([^\\s:]*)\\s*:\\s?(.*)";
        Pattern p = Pattern.compile(pattern);
        for (String person : persons) {
            Matcher matcher = p.matcher(person);
            if (matcher.find()) {
                String name = matcher.group(1);
                String mobile = matcher.group(2);
                System.out.printf("이름 : %s, 휴대전화번호 : %s%n", name, mobile);
            }
        }
    }
}
```

![image](https://github.com/somi9954/Java/assets/137499604/45830e5a-3220-47b4-9341-5eed7c8b2c5e)

[참고하기](https://moonong.tistory.com/31)
