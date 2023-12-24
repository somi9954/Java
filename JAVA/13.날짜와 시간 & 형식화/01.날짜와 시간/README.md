# 날짜와 시간

## Calendar 와 Date 클래스

- 날짜와 시간 정보를 제공해주는 클래스에는  Date 클래스와  Calendar클래스가 있다.
- 최근 날짜를 표현할때 Date 클래스보다는 Calendar 클래스를 사용하는것을 권장한다. ⇒ Date 클래스의 많은 기능이 종료를 기다리고 있기 때문이다.

```text
💡 Date 클래스와 Calendar클래스
˙ Date 클래스 : 특정 시점의 날짜를 표현하는 클래스로 날짜와 시간 정보를 저장(JDK 1.0부터)
˙ Calendar클래스 : 달력을 표현한 클래스로 운영체제의 날짜와 시간 정보를 얻음(JDK 1.1부터)
```

- Calendar는 Date보다는 낳았지만 몇가지 단점들이 발견 되어 JDK1.8부터 **java.time 패키지**로 기존의 단점을 개선한 새로운 클래스들이 추가 되었다.

### **Calendar와 GregorianCalendar**

- Calendar 클래스는 추상클래스이기 때문에 다른 객체 선언처럼 new 키워드를 사용하여 선언하지 않고, 생성된 인스턴스를 받아오는 형식으로 선언해야 한다.

```java
Calendar cal = new Calendar(); //에러 -> 추상클래스는 인스턴스 생성불가
 Calendar cal = calendar.getTnstance(); //ok ->getInstance()메소드는 Calendar를 구현한 
//클래스의 인스턴스를 반환한다.
```

- Calendar를 상속받아 완전히 구현한 클래스로는 GregorianCalendar와 BuddhistCalendar가 있다.
- getInstance()는 시스템의 국가와 지역설정을 확인해서 태국인 경우에는 BuddhistCalendar의 인스턴스를 반환하고, 그 외에는 GregorianCalendar와 인스턴스를 반환한다.
- GregorianCalendar는 Calendar를 상속받아 오늘날 전세계 공통으로 사용하고 있는 그레고리력에 맞게 구현한 것으로 태국을 제외한 나머지 국가에서는 GregorianCalendar를 사용하면 된다.
- 인스턴스를 직접 생성해서 사용하지 않고 메소드를 통해서 인스턴스를 반환받게 하는 이유는 최소한의 변경으로 프로그램이 동작할 수 있도록 하기 위한 것이다.

```java
class MyApplication {
	public static void main(String[] args) {
		Calendar cal = new GregorianCalendar(); // 경우에 따라 이 부분을 변경해야 한다.
		...
	}
}

```

- 상기 코드와 같이 특정 인스턴스를 생성하도록 프로그램이 작성되어 있다면, 다른 종류의 역법(calendar)을 사용하는 국가에서 실행되거나, 새로운 역법이 추가된다면, 즉 다른 종류의 인스턴스를 필요로 하는 경우에 MyApplication을 변경해야 한다.

```java
class MyApplication {
	public static void main(String[] args) {
		Calendar cal = Calendar.getInstance();
		...
	}
}

```

- getIntance()를 사용하면 구현되는 내용은 달라지겠지만 MyApplication이 변경되지 않아도 된다.
- getInstance()메서드가 static인 이유는 메서드 내의 코드에서 인스턴스 변수를 사용하거나 인스턴스 메서드를 호출하지 않기 때문
- Calenda는 추상 클래스 이므로 객체를 생성할 수 없다, 따라서 객체를 생성하기 위한 static 메서드은 getInstance()가 필요하다.

### **Calendar 클래스의 속성**

- 여러가지의 상수 필드들이 존재한다. 날짜를 표기하기 위해 자주 사용하는 값들을 상수화하여 관리한다.
- 대표적으로 사용하는 상수값은 다음과 같다.

| 상수 | 사용방법 | 설명 |
| --- | --- | --- |
| static int YEAR | Calendar.YEAR | 현재 년도 |
| static int MONTH | Calendar.MONTH | 현재 월 (1월: 0) |
| static int DATE | Calendar.DATE | 현재 월의 날짜 |
| static int WEEK_OF_YEAR | Calendar.WEEK_OF_YEAR | 현재 년도의 몇째 주 |
| static int WEEK_OF_MONTH | Calendar.WEEK_OF_MONTH | 현재 월의 몇째 주 |
| static int DAY_OF_YEAR | Calendar.DAY_OF_YEAR | 현재 년도의 날짜 |
| static int DAY_OF_MONTH | Calendar.DAY_OF_MONTH | 현재 월의 날짜 |
| static int DAY_OF_WEEK | Calendar.DAY_OF_WEEK | 현재 요일(일요일:1 ,토요일: 7) |
| static int HOUR | Calendar.HOUR | 현재 시간 (12시간제) |
| static int HOUR_OF_DAY | Calendar.HOUR_OF_DAY | 현재 시간 (24시간제) |
| static int MINUTE | Calendar.MINUTE | 현재 분 |
| static int SECOND | Calendar.SECOND | 현재 초 |

## Calendar 클래스의 주요 메소드

| 메소드 | 설명 |
| --- | --- |
| static Calendar getInstance() | 현재 날짜와 시간 정보를 가진 Calendar 객체를 생성한다. |
| boolean after(Object when) | when과 비교하여 현재 날짜 이후이면 true, 아니면 false를 반환한다. |
| boolean before(Object when) | when과 비교하여 현재 날짜 이전이면 true, 아니면 false를 반환한다. |
| boolean equals(Object obj) | 같은 날짜값인지 비교하여 true, false를 반환한다. |
| int get(int field) | 현재 객체의 주어진 값의 필드에 해당하는 상수 값을 반환한다.이 상수값은 Calendar 클래스의 상수중에 가진다. |
| Date getTime() | 현재의 객체를 Date 객체로 변환한다. |
| long getTimeInMills() | 객체의 시간을 1/1000초 단위로 변경하여 반환한다. |
| void set(int field, int value) | 현재 객체의 특정 필드를 다른 값으로 설정한다. |
| void set(int year, int month, int date) | 현재 객체의 년, 월, 일 값을 다른 값으로 설정한다. |
| void set(int year, int month, int date, int hour, int minute, int second) | 현재 객체의 년, 월, 일, 시, 분, 초 값을 다른 값으로 설정한다. |
| void setTime(Date date) | date 객체의 날짜와 시간 정보를 현재 객체로 생성한다. |
| void setTimeInMills(long mills) | 현재 객체를 1/1000초 단위의 주어진 매개변수 시간으로 설정한다. |
| int getActualMinimum(int field) | 현재 객체의 특정 필드의 최소 값을 반환한다. |
| int getActualMaximum(int field) | 현재 객체의 특정 필드의 최대 값을 반환한다. |
- Calendar 클래스를 이용해 달력 만들기

```java
package section15;
import java.util.Calendar;
import java.util.Scanner;

public class EX15_17 {
	public static void main(String[] args) {
		// Calendar 객체 생성 (오늘의 정보)
		Calendar cal = Calendar.getInstance();
		
		Scanner scan = new Scanner(System.in);
		
		System.out.println("연도를 입력하세요");
		int year = scan.nextInt();
		
		System.out.println("월을 입력하세요");
		int month = scan.nextInt();
		
		// Calendar 클래스는 월의 시작이 0부터 시작
		cal.set(year, month - 1, 1);
		
		System.out.printf("일\t월\t화\t수\t목\t금\t토\n");
		// 달의 마지막 날짜를 구함
		int lastOfDate = cal.getActualMaximum(Calendar.DATE);
		// 지정한 달의 시작하는 요일을 구함
		int week = cal.get(Calendar.DAY_OF_WEEK);
		
		// 달력 시작 날의 주말 처리
		for(int i = 1; i < week; i++) {
			System.out.print("\t");
		}
		
		for(int i = 1; i <= lastOfDate; i++) {
			System.out.printf("%d\t", i);
			// 토요일에 날짜를 표시하고 줄 바꿈 하는 코드
			if(week % 7 == 0) {
				System.out.println();
			}
			week++;
		}
		
		scan.close();
	}
}
```

<img src="https://github.com/somi9954/Java/assets/137499604/6bcf403a-4d03-4568-a11a-aede189ff6f1" width="300" height="300">

### Date와 Calendar간의 변환

- Calendar가 새로 추가되면서 Date는 대부분의 메서드가 'dreprecated' 되었으므로 잘 사용되지 않는다.
- 그러나 여전히 Date를 필요로 하는 메서드들이 있기 때문에 Calendar를 Date로 또는 그 반대로 변환할 일이 있다.
    - Calendar를 Date로 변환
    
    ```java
     Calendar cal = Calendar.getInstance();
     ...
     Date d = new Date(cal.getTimeInMillis()); // Date(long date)
    
    ```
    
    - Date를 Calendar로 변환
    
    ```java
     Date d = new Date();
     ...
     Calendar cal = Calendar.getInstance();
     cal.setTime(d);
    
    ```
    

```java
package day12.date_calendar;

import java.util.*;

public class CalendarEx1 {
	public static void main(String[] args) {
		// 기본적으로 현재날짜와 시간으로 설정된다.
		Calendar today = Calendar.getInstance();

		System.out.println("이 해의 년도 : " + today.get(Calendar.YEAR));
		System.out.println("월(0~11, 0:1월) : " + today.get(Calendar.MONTH));
		System.out.println("이 해의 몇 째 주 : " + today.get(Calendar.WEEK_OF_YEAR));
		System.out.println("이 달의 몇 째 주 : " + today.get(Calendar.WEEK_OF_MONTH));

		// DATE와 DAY_OF_MONTH와는 같다.
		System.out.println("이 달의 몇 일 : "+ today.get(Calendar.DATE));
		System.out.println("이 달의 몇 일 : "+ today.get(Calendar.DAY_OF_MONTH));
		System.out.println("이 해의 몇 일 : "+ today.get(Calendar.DAY_OF_YEAR));
		System.out.println("요일(1~7), 1:일요일  : "+ today.get(Calendar.DAY_OF_WEEK)); // 1. 일요일, 2. 월요일 ... 7.토요일
		System.out.println("이 달의 몇 째 요일 : "+ today.get(Calendar.DAY_OF_WEEK_IN_MONTH));
		System.out.println("오전_오후(0:오전, 1:오후) : "+ today.get(Calendar.AM_PM));
		System.out.println("시간(0~11) : "+ today.get(Calendar.HOUR));
		System.out.println("시간(0~23) : "+ today.get(Calendar.HOUR_OF_DAY));
		System.out.println("분(0~59) : "+ today.get(Calendar.MINUTE));
		System.out.println("초(0~59) : "+ today.get(Calendar.SECOND));
		System.out.println("1000분의 1초(0~999)  : "+ today.get(Calendar.MILLISECOND));

		System.out.println("TimeZone(~12~+12): " + (today.get(Calendar.ZONE_OFFSET) / (60 * 60 * 1000)));
		System.out.println("이 달의 마지막 날:" + today.getActualMaximum(Calendar.DATE));
	}
}

실행결과
이 해의 년도 : 2022
월(0~11, 0:1월) : 4
이 해의 몇 째 주 : 19
이 달의 몇 째 주 : 1
이 달의 몇 일 : 5
이 달의 몇 일 : 5
이 해의 몇 일 : 125
요일(1~7), 1:일요일  : 5
이 달의 몇 째 요일 : 1
오전_오후(0:오전, 1:오후) : 0
시간(0~11) : 9
시간(0~23) : 9
분(0~59) : 56
초(0~59) : 58
1000분의 1초(0~999)  : 207
TimeZone(~12~+12): 9
이 달의 마지막 날:31

```

- getInstance(),를 통해서 얻은 인스턴스는 기본적으로 현재 시스템의 날짜와 시간에 대한 정보를 담고 있다.
- 원하는 날짜나 시간으로 설정하려면 **set 메서드 ** 사용
- 원하는 필드의 값을 얻어오려면 **int get(int field)**를 사용
- get(Calendar.MONTH)로 얻어오는 값의 범위는 0~11이다. 즉 0은 1월, 11은 12월을 의미한다.

```java
package day12.date_calendar;

import java.util.Calendar;

public class CalendarEx2 {
	public static void main(String[] args) {
		// 요일은 1부터 시작하기 때문에, DAY_OF_WEEK[0]은 비워두었다.
		final String[] DAY_OF_WEEK = {"", "일", "월", "화", "수", "목", "금", "토" };

		Calendar date1 = Calendar.getInstance();
		Calendar date2 = Calendar.getInstance();

		// month의 경우 0부터 시작하기 때문에 8월인 경우 7로 지정해야 한다.
		// date1.set(2021, Calendar.AUGUST, 15); 와 같이 할 수 도 있다.
		date1.set(2021, 7, 15); // 2021년 8월 15일
		System.out.println("date1은 " + toString(date1) +  DAY_OF_WEEK[date1.get(Calendar.DAY_OF_WEEK)] + "요일 이고, ");
		System.out.println("오늘(date2)은 " + toString(date2) +  DAY_OF_WEEK[date2.get(Calendar.DAY_OF_WEEK)] + "요일 이고, ");

		// 두 날짜 사이의 차이를 얻으려면, getTimeInMillis() 천분의 일초 단위로 변환해야 한다.
		long difference = (date2.getTimeInMillis() - date1.getTimeInMillis()) / 1000;
		System.out.println("그 날(date1)부터 지금(date2)까지 " + difference + "초가 지났습니다.");
		System.out.println("월(day)로 계산하면 " + difference / (24*60 * 60) + "일 입니다."); // 1일 - 24 * 60 * 60
	}

	public static String toString(Calendar date) {
		return date.get(Calendar.YEAR) + "년 " + (date.get(Calendar.MONTH) + 1) + "월 " + date.get(Calendar.DATE) + "일";
	}
}

실행결과
date1은 2021년 8월 15일일요일 이고,
오늘(date2)은 2022년 5월 5일목요일 이고,
그 날(date1)부터 지금(date2)까지 22723200초가 지났습니다.
월(day)로 계산하면 263일 입니다.

```

- 날짜와 시간을 원하는 값으로 변경하려면 set메서드를 사용

```java
void set (int field, int value)
void set(int year, int month, int date)
void set(int year, int month, int date, int hourOfDay, in minute)
void set(int year, int month, int date, int hourOfDay, in minute, int second)

```

- 시간상 전후를 알고 싶을 때는 두 날짜간의 차이가 양수인지 음수인질을 판단하면 된다.
- 또는 간단히 boolean after(Object when)과 boolean before(Object when)을 사용해도 된다.

```java
package day12.date_calendar;

import java.util.*;

public class CalendarEx3 {
	public static void main(String[] args) {
		Calendar date = Calendar.getInstance();
		date.set(2021, 7, 31); // 2021년 8월 31일

		System.out.println(toString(date));
		System.out.println("= 1일 후 =");
		date.add(Calendar.DATE, 1);
		System.out.println(toString(date));

		System.out.println("= 6달 전 =");
		date.add(Calendar.MONTH, -6);
		System.out.println(toString(date));

		System.out.println("= 31일 후(roll) =");
		date.roll(Calendar.DATE, 31);
		System.out.println(toString(date));

		System.out.println("= 31일 후(add) =");
		date.add(Calendar.DATE, 31);
		System.out.println(toString(date));
	}

	public static String toString(Calendar date) {
		return date.get(Calendar.YEAR) + "년 " + (date.get(Calendar.MONTH) + 1) + "월 " + date.get(Calendar.DATE) + "일";
	}
}

실행결과
2021년 8월 31일
= 1일 후 =
2021년 9월 1일
= 6달 전 =
2021년 3월 1일
= 31일 후(roll) =
2021년 3월 1일
= 31일 후(add) =
2021년 4월 1일

```

- add(int field, int amount)를 사용하면 지정한 필드의 값을 원하는 만큼 증가 또는 감소 시킬수 있다.
- roll(int field, int amount)도 지정한 필드의 값을 증가 또는 감소시킬 수 있는데, add메서드와의 차이점은 다른 필드에 영향을 미치지 않는다는 것 예를 들어 add메서드로 날짜 필드(Calendar.MONTH)의 값을 31만큼 증가시켰다면 다음 달로 넘어가므로 월 필드(Calendar.MONTH)의 값도 1이 증가하지만, roll 메서드는 같은 경우에 월 필드의 값은 변하지 않고 일 필드의 값만 바뀐다.

```java
package day12.date_calendar;

import java.util.*;

public class CalendarEx4 {
	public static void main(String[] args) {
		Calendar date = Calendar.getInstance();

		date.set(2021, 0, 31); // 2021년 1월 31일
		System.out.println(toString(date));
		date.roll(Calendar.MONTH, 1);
		System.out.println(toString(date));
	}

	public static String toString(Calendar date) {
		return date.get(Calendar.YEAR) + "년 " + (date.get(Calendar.MONTH) + 1) + "월 " + date.get(Calendar.DATE) + "일";
	}
}

실행결과
2021년 1월 31일
2021년 2월 28일

```
