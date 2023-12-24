# java.time 패키지

- Date와 Calendar가 가지고 있는 단점들을 해소하기 위해 JDK1.8부터 'java.time 패키지'가 추가되었다.
- 이 패키지는 다음과 같이 4개의 하위 패키지를 가지고 있다

| 패키지 | 설명 |
| --- | --- |
| java.time | 날짜와 시간을 다루는데 필요한 핵심 클래스들을 제공 |
| java.time.chrono | 표준(ISO)이 아닌 달력 시스템을 위한 클래스들을 제공 |
| java.time.format | 날짜와 시간을 파싱하고, 형식화하기 위한 클래스들을 제공 |
| java.time.temporal | 날짜와 시간의 필드(field)와 단위(unit)을 위한 클래스들을 제공 |
| java.time.zone | 시간대(time-zone)와 관련된 클래스들을 제공 |
- 상기 패키지들에 속한 클래스들의 가장 큰 특징은 String클래스 처럼 불변(immutable)이라는 것이다.
- 그래서 날짜나 시간을 변경하는 메서드들은 기존의 객체를 변경하는 대신 항상 변경된 새로운 객체를 반환한다.
- 기존 Calendar 클래스는 변경이 가능하므로, 멀티 쓰레드 환경에서 안전하지 못하다.

## java.time 패키지의 핵심 클래스

- 날짜와 시간을 하나로 표현하는 Calendar 클래스와 달리, java.time 패키지에서는 날짜와 시간을 별도 클래스로 분리해 놓았다.
- LocalTime 클래스 : 시간을 표현
- LocalDate 클래스 : 날짜를 표현
- LocalDateTime 클래스 : 날짜와 시간을 모두 표현

```java
LocalDate(날짜) + LocalTime(시간) -> LocalDateTime(날짜 & 시간)

```

- ZonedDateTime 클래스 : LocalDateTime + 시간대
- Instant 클래스 : 날짜와 시간을 초 단위(정확히는 나노초)로 표현한다.
    
    날짜와 시간을 초단위로 표현한 값을 타임스탬프(time-stamp)라고 부르는데, 이 값은 날짜와 시간을 하나의 정수로 표현할 수 있으므로 날짜와 시간의 차이를 계산하거나 순서비를 비교하는데 유리하다.
    
- 기타 : Year, YearMonth, MonthDay 클래스

### Period와 Duration (TemporaAmount 인터페이스)

- Period 클래스 - 두 날짜 간의 차이를 표현하기 위한 것
- Double 클래스 - 시간의 차이를 표현하기 위한 것

```java
날짜 - 날짜 = Period
시간 - 시간 = Duration

```

### 객체 생성하기 - now(), of()

- now() : 현재 날짜와 시간을 저장하는 객체를 생성한다.

```java
LocalDate date = LocalDate.now(); // 현재 날짜
LocalTime time = LocalTime.now(); // 현재 시간
LocalDateTime dateTime = LocalDateTime.now(); // 현재 날짜와 시간
ZonedDateTime dateTimeInKr = ZonedDateTime.now(); // 현재 날짜와 시간 + 시간대

```

- of() : 지정된 날짜, 시간, 시간대의 객체를 생성한다.

```java
LocalDate date = LocalDate.of(2021,11,23); // 2021년 11월 23일
LocalTime time = LocalTime.of(23,59,59); // 23시 59분 59초

LocalDateTime dateTime = LocalDateTime.of(date, time);
ZonedDateTime zDateTime = ZonedDateTime.of(dateTime, ZoneId.of("Asia/Seoul"));

```

### Temporal과 TemporalAmount

- LocalDate, LocalTime, LocalDateTime, ZonedDateTime등 날짜와 시간을 표현하기 위한 클래스들은 모두 **Temporal, TemporalAccessor, TemporalAdjuster 인터페이스**를 구현하였다.
- Duration과 Period는 **TemporalAmount 인터페이스**를 구현하였다.

```java
Temporal, TemporalAccessor, TemporalAdjuster를 구현한 클래스
	- LocalDate, LocalTime, LocalDateTime, ZonedDateTime, Instant 등

TemporalAmount를 구현한 클래스
	- Period, Duration

```

### TemporalUnit과 TemporalField

- TemportalUnit 인터페이스 : 날짜와 시간의 단위를 정의해 놓은 것, 이 인터페이스를 구현한 것이 **열거형 ChronoUnit**이다.
- TemporalFIeld 인터페이스 : 년, 월, 일 등의 날짜와 시간의 필드를 정의해 놓은 것, 이 인터페이스를 구현한 것이 **열거형 ChronoField**이다.

```java
LocalTime now = LocalTime.now(); // 현재 시간
int minute = now.getMinute(); // 현재 시간에서 분(minute)만 추출
int minute = now.get(ChronoField.MINUTE_OF_HOUR); // now.getMinute()와 동일

```

- 날짜와 시간에서 틀정 필드의 값만 얻을 때는 get()이나 get으로 시작하는 이름의 메서드를 이용한다.
- 특정 날자의 시간에서 지정된 단위의 값을 더하거나 뺄 때는 plus() 또는 minus()에 값과 함께 열거형 ChonoUnit을 사용한다.

```java
int get(TemporalField field)
LocalDate plus(long amountToAdd, TemporalUnit unit)

```

```java
LocalDate today = LocalDate.now(); // 오늘
LocalDate tomorrow = today.plus(1, ChronoUnit.DAYS); // 오늘에 1일을 더한다.
LocalDate tomorrow = today.plusDays(1); // today.plus(1, ChronoUnit.DAYS)와 동일

```

- isSupported() : TemporalField나 TemporalUnit을 사용할 수 있는지 확인하는 메서드

```java
boo
lean isSupported(TemporalUnit unit)  // Temporal에 정의
boolean isSupported(TemporalField field) // TemporalAccessor에 정의

```

## LocalDate와 LocalTime

- LocalDate와 LocalTime은 java.time 패키지의 가장 기본이 되는 클래스이다.
- 나머지 클래스 들은 이 두 클래스의 확장이다.
- now() : 현재의 날짜와 시간을 LocalDate와 LocalTime으로 각각 반환한다.

```java
LocalDate today = LocalDate.now(); // 오늘의 날짜
LocalTime now = LocalTime.now(); // 현재 시간

LocalDate birthDate = LocalDate.of(2021, 12, 31); // 2021년 12월 31일
LocalTime birthTime = LocalTime.of(23, 59, 59); // 23시 59분 59초

```

- of() : 지정된 날짜와 시간으로 LocalDate와 LocalTime 객체를 생성한다.

```java
static LocalDate of(int year, Month month, int dayOfMonth)
static LocalDate of(int year, int month, int dayOfMonth)

static LocalTime of(int hour, int min)
static LocalTime of(int hour, int min, int sec)
static LocalTime of(int hour, int min, int sec, int nanoOfSecond)

```

- 일 단위 또는 초 단위로 시간을 지정할 수 있다.

```java
// 1999년의 365번째 날
LocalDate birthDate = LocalDate.ofYearDay(1999, 365); // 1999년 12월 31일

// 오늘 0시 0분 0초 부터 86399초(하루는 86400초)가 지난 시간
LocalTime birthTime = LocalTime.ofSecondDay(86399); // 23시 59분 59초

```

- parse() : 문자열을 날짜와 시간으로 변환할 수 있다.

```java
LocalDate birthDate = LocalDate.parse("1999-12-31");
LocalTime birthTime = LocalTime.parse("23:59:59");

```

### 특정 필드의 값 가져오기 - get(), getXXX()

- 주의할 점 : Calendar와 달리 월(month)의 범위가 1~12이고, 요일은 월요일이 1, 화요일이 2, ..., 일요일은 7이라는 것이다.
- LocalDate

| 메서드 | 설명(1999-12-31 23:59:59) |
| --- | --- |
| int getYear() | 년도(1999) |
| int getMonthValue() | 월(12) |
| Month getMonth() | 월(DECEMBER) getMonth().getValue() = 12 |
| int getDayOfMonth() | 일(31) |
| int getDayOfYear() | 같은 해의 1월 1일부터 몇번째 일(365) |
| DayOfWeek getDayOfWeek() | 요일(FRIDAY) getDayOfWeek().getValue() = 5 |
| int lengthOfMonth() | 같은 달의 총 일수(31) |
| int lengthOfYear() | 같은 해의 총 일수(365), 윤년이면 366 |
| boolean isLeapYear() | 윤년 여부 확인(false) |
- LocalTime

| 메서드 | 설명(1999-12-31 23:59:59) |
| --- | --- |
| int getHour() | 시(23) |
| int getMinute() | 분(59) |
| int getSecond() | 초(59) |
| int getNano() | 나노초(0) |
- get(), getLong() : 원하는 필드를 직접 지정할 수 있다대부분의 필드는 int타입의 범위에 속하지만, 몇몇 필드는 int타입의 범위를 넘어서는데, 그때에는 get()대신 getLong()을 사용한다. 하기 표는 ChronoField에 정의된 상수 목록이며 getLong을 사용해야 하는 경우는 *표 표기 하였다.

| TemporalField(ChronoField) | 설명 |
| --- | --- |
| ERA | 시대 |
| YEAR_OF_ERA, YEAR | 년 |
| MONTH_OF_YEAR | 월 |
| DAY_OF_WEEK | 요일(1:월요일, 2:화요일, ... 7:일요일) |
| DAY_OF_MONTH | 일 |
| AMPM_OF_DAY | 오전/오후 |
| HOUR_OF_DAY | 시간(0~23) |
| CLOCK_HOUR_OF_DAY | 시간(1~24) |
| HOUR_OF_AMPM | 시간(0~11) |
| CLOCK_HOUR_OF_AMPM | 시간(1~12) |
| MINUTE_OF_HOUR | 분 |
| SECOND_OF_MINUTE | 초 |
| MILLI_OF_SECOND | 천분의 일초 |
| MICRO_OF_SECOND * | 백만분의 일초 |
| NANO_OF_SECOND * | 10억분의 일초 |
| DAY_OF_YEAR | 그 해의 몇번째날 |
| EPOCH_DAY * | EPOCH(1970.1.1)부터 몇번째 날 |
| MINUTE_OF_DAY | 그 날의 몇 번째 분(시간을 분으로 환산) |
| SECOND_OF_DAY | 그 날의 몇 번째 초(시간을 초로 환산) |
| MILL_OF_DAY | 그날의 몇번째 몇 번째 밀리초 |
| MICRO_OF_DAY * | 그날의 몇 번째 마이크로 초 |
| NANO_OF_DAY * | 그날의 몇 번째 나노초 |
| ALIGNED_WEEK_OF_MONTH | 그 달의 n번째 주 |
| ALIGNED_WEEK_OF_YEAR | 그 해의 n번째 주 |
| ALIGNED_DAY_OF_WEEK_IN_MONTH | 요일(그 달의 1일을 월요일로 간주하여 계산) |
| ALIGNED_DAY_OF_WEEK_IN_YEAR | 요일(그 해의 1월 1일을 월요일로 간주하여 계산) |
| INSTANT_SECONDS | 년월일을 초단위로 환산(1970-01-01 00:00:00 UTC를 0초로 계산) Instant에만 사용가능 |
| OFFSET_SECONDS | UTC와 시차. ZoneOffset에만 사용가능 |
| PROLEPTIC_MONTH | 년월을 월단위로 환산(2015년11월 = 2015*12+11) |
- 상기 목록은 ChonoField에 정의된 모든 상수를 나열하였으나, 사용할 수 있는 필드는 클래스마다 다르다(예 : LocalDate는 날짜를 표현하기 위한 것이므로, MINUTE_OF_HOUR와 같이 시간에 관련된 필드는 사용할 수 없다)
- 해당 클래스가 지원하지 않는 필드를 사용하면 UnsupportedTemporalTypeException이 발생한다.
- range() : 특정 필드가 가질 수 있는 값의 범위를 조회

```java
System.out.println(ChronoField.CLOCK_HOUR_OF_DAY.range()); // 1 - 24
System.out.println(ChronoField.HOUR_OF_DAY.range()); // 0 - 23

```

### 필드의 값 변경하기 - with(), plus(), minus()

### with()

- 날짜와 시간에서 특정 필드 값을 변경하려면, 하기와 같이 with로 시작하는 메서드를 사용한다.

```java
LocalDate withYear(int year)
LocalDate withMonth(int month)
LocalDate withDayOfMonth(int dayOfMonth)
LocalDate withDayOfYear(int dayOfYear)

LocalTime withHour(int hour)
LocalTime withMinute(int minute)
LocalTime withSecond(int second)
LocalTime withNano(int nanoSecond)

```

- with()를 사용하면 원하는 필드를 직접 지정할 수 있다.

```java
LocalDate with(TemporalField field, long newValue)

```

```java
date = date.withYear(2000); 년도를 2000년으로 변경
time = time.withHour(12); // 시간을 12시로 변경

```

### plus(), minus()

- 특정 필드에 값을 더하거나 뺄때

```java
LocalTime plus(TemporalAmount amountToAdd);
LocalTime plus(long amountToAdd, TemporalUnit unit)

LocalDate plus(TemporalAmount amountToAdd)
LocalDate plus(long amountToAdd, TemporalUnit unit)

```

- plus()로 만든 메서드

```java
LocalDate plusYears(long yearsToAdd)
LocalDate plusMonths(long monthToAdd)
LocalDate plusDays(long daysToAdd)
LocalDate plusWeeks(long weeksToAdd)

LocalTime plusHours(long hoursToAdd)
LocalTime plusMinutes(long minutesToAdd)
LocalTime plusSeconds(long secondsToAdd)
LocalTime plusNanos(long nanoToAdd)

```

### LocalTime의 truncatedTo()

- 지정된 것보다 작은 단위의 필드를 0으로 만든다.

```java
LocalTime time = LocalTime.of(12, 34, 56); // 12시 34분 56초
time = time.truncatedTo(ChronoUnit.HOURS); // 시(hours)보다 작은 단위를 0으로 만든다
System.out.println(time); // 12:00

```

- LocalDate에 truncatedTo()는 없다. LocalDate의 필드인 년, 월, 일은 0이 될수 없다.

### ChronoUnit에 정의된 상수 목록

| TemporalUnit(ChronoUnit) | 설명 |
| --- | --- |
| FOREVER | Long.MAX_VALUE초(약 3천억년) |
| ERAS | 1,000,000,000년 |
| MILLENNIA | 1,000년 |
| CENTURIES | 100년 |
| DECADES | 10년 |
| YEARS | 년 |
| MONTHS | 월 |
| WEEKS | 주 |
| DAYS | 일 |
| HALF_DAYS | 반나절 |
| HOURS | 시 |
| MINUTES | 분 |
| SECONDS | 초 |
| MILLIS | 천분의 일초 |
| MICROS | 백만분의 일초 |
| NANOS | 10억분의 일초 |

### 날짜와 시간의 비교 - isAfter(), isBefore(), isEqual()

- LocalDate와 LocalTime도 compareTo()가 적절하게 재정의 되어 있어, 하기와 같이 compareTo()로 비교할 수 있다.

```java
int result = date1.compareTo(date2); // 같으면 0, date1이 이전이면 -1, 이후면 1

```

- 그러나 보다 편하하게 비교할 수 있는 메서드들이 추가로 제공된다.

```java
boolean isAfter(ChronoLocalDate other)
boolean isBefore(ChronoLocalDate other)
boolean isEqual(ChronoLocalDate other) // LocalDate에만 있음

```

```java
package day12.time;

import java.time.*;
import java.time.temporal.*;

public class NewTimeEx1 {
	public static void main(String[] args) {
		LocalDate today = LocalDate.now(); // 오늘의 날짜
		LocalTime now = LocalTime.now(); // 현재의 시간

		LocalDate birthDate = LocalDate.of(1999, 12, 31); // 1999년 12월 31일
		LocalTime birthTime = LocalTime.of(23, 59, 59); // 23시 59분 59초

		System.out.println("today=" + today);
		System.out.println("now=" + now);
		System.out.println("birthDate=" + birthDate);  // 1999-12-31
		System.out.println("birthTime=" + birthTime); // 23:59:59

		System.out.println(birthDate.withYear(2000)); // 2000-12-31
		System.out.println(birthDate.plusDays(1)); // 2000-01-01
		System.out.println(birthDate.plus(1, ChronoUnit.DAYS)); // 2000-01-01

		// 23:59:59 -> 23:00
		System.out.println(birthTime.truncatedTo(ChronoUnit.HOURS));

		// 특정 ChronoField의 범위를 알아내는 방법
		System.out.println(ChronoField.CLOCK_HOUR_OF_DAY.range()); // 1-24
		System.out.println(ChronoField.HOUR_OF_DAY.range()); // 0-23
	}
}

실행결과
today=2022-05-05
now=18:51:40.110864700
birthDate=1999-12-31
birthTime=23:59:59
2000-12-31
2000-01-01
2000-01-01
23:00
1 - 24
0 - 23

```

## Instant

- Instant는 에포크 타입(EPOCH TIME, 1970-01-01 00:00:00 UTC)부터 경과된 시간을 나노초 단위로 표현한다.
- Instant를 생성할 때는 위와 같이 now()와 ofEpochSecond()를 사용한다.

```java
Instant now = Instant.now();
Instant now2 = nstant.ofEpochSecond(now.getEpochSecond());
Instant now3 = Instant.ofEpochSecond(now.getEpochSecond(), now.getNano());

```

- 필드에 저장된 값을 가져올때는 하기와 같이 한다.

```java
long epochSec = now.getEpochSecond();
int nano = now.getNano();

```

- 타임스탬프(timestamp)처럼 밀리초 단위의 EPOCH TIME을 필요로 하는 경우

```java
long toEpochMilli()

```

- Instant는 항상 UTC(+00:00)를 기준으로 하기 때문에 LocalTime과 차이가 있을 수 있다.(예 : 한국은 시간대가 +09:00이므로 Instant와 LocalTime간에는 9시간의 차이가 있다.)
    
    > UTC는 'Coordincated Universal Time'의 약어로 '세계 협정시'이라고 하며, 1972년 1월 1일부터 시행된 국제 표준시이다. 이전에 사용되던 GMT(Greenwich Mean Time)와 UTC는 거의 같지만, UTC가 좀 더 정확하다.
    > 

### Instant와 Date간의 변환

Instant는 기존의 java.util.Date를 대체하기 위한 것이며, JDK1.8부터 Date에 Instant로 변환할 수 있는 새로운 메서드가 추가되었다.

```java
static Date from(Instant instant)  // Instant -> Date
Instant toInstant()  // Date -> Instant

```

## LocalDateTime과 ZonedDateTime

- LocalDate에 LocalTime을 합쳐 놓은 것이 LocalDateTime이다.
- LocalDateTime에 시간대(time zone)을 추가한 것이 ZonedDateTime이다.

```java
LocalDate + LocalTime -> LocalDateTime
LocalDateTime + 시간대 -> ZonedDateTime

```

### LocalDate와 LocalTime으로 LocalDateTime만들기

- LocalDate와 LocalTime을 합쳐서 만들기

```java
LocalDate date = LocalDate.of(2021, 12, 31);
LocalTime time = LocalTime.of(12, 34, 56);

LocalDateTime dt = LocalDateTime.of(date, time);
LocalDateTIme dt2 = date.atTime(time);
LocalDateTime dt3 = time.atDate(date);
LocalDateTime dt3 = date.atTime(12, 34, 56);
LocalDateTime dt4 = time.atDate(LocalDate.of(2021, 12, 31));
LocalDateTime dt6 = date.atStartOfDay(); // dt6 = date.atTime(0, 0, 0);

```

- of() - 날짜와 시간을 직접 지정, now() - 현재 날짜와 시간

```java
// 2021년 12월 31일 12시 34분 56초
LocalDateTime dateTime = LocalDateTime.of(2021, 12, 31, 12, 34, 56);

LocalDateTime today = LocalDateTime.now();

```

### LocalDateTime의 변환

```java
LocalDateTime dt = LocalDateTime.of(2021, 12, 31, 12, 34, 56);
LocalDateTime date = dt.toLocalDate(); // LocalDateTime -> LocalDate
LocalTime time = dt.toLocalTime(); // LocalDateTime -> LocalTime

```

### LocalDateTime으로 ZonedDateTime 만들기

- LocalDateTIme에 시간대(time-zone)을 추가하면, ZonedDateTime이 된다. 기존에는 TimeZone클래스로 시간대를 다뤘지만 새로운 시간 패키지에서는 ZoneId라는 클래스를 사용한다.
- ZoneId는 일광 절약시간(DST, Daylight Saving Time)을 자동적으로 처리해 주므로 편리하다.
- LocalDateTime에 atZone()으로 시간대 정보를 추가하면, ZonedDateTime을 얻을 수 있다.

> 사용가능한 ZoneId의 목록은 ZoneId.getAvailableZoneIds()로 얻을 수 있다.
> 

```java
ZoneId zid = ZoneId.of("Asia/Seoul");
ZonedDateTime zdt = dateTime.atZone(zid);

```

- LocalDate의 asStartOfDate() 메서드에 매개변수로 ZoneId를 지정하는 방법

```java
ZoneId zid = ZoneId.of("Asia/Seoul");
ZonedDateTime zdt = LocalDate.now().atStartOfDay(zid);

```

- 특정 시간대의 시간을 알고 싶을 경우

```java
예: 뉴욕의 현재 시간을 알고 싶은 경우

ZoneId nyId = ZoneId.of("America/New_York");
ZonedDateTime nyTime = ZonedDateTime.now().withZoneSameInstant(nyId);

- 상기 코드에서 now() 대신 of를 사용하면 날짜와 시간을 지정할 수 있다.

```

### ZonedOffset

- UTC로 부터 얼마만큼 떨어져 있는지를 ZoneOffset으로 표현한다.

```java
ZoneOffset krOffset = ZonedDateTime.now().getOffset();
ZoneOffset krOffset = ZoneOffset.of("+9");
int krOffsetInSec = krOffset.get(ChronoField.OFFSET_SECONDS); // 32400초

```

### OffsetDateTime

- ZonedDateTime은 ZonedId로 구역을 표현하는데, ZoneId가 아닌 ZoneOffset을 사용하는 것이 OffsetDateTime이다.
- ZoneId는 일광절약시간처럼 시간대와 관련된 규칙들을 포함하고 있는데, ZoneOffset은 단지 시간대를 시간의 차이로만 구분한다.
- 서로 다른 시간대에 존재하는 컴퓨터간의 통신에는 OffsetDateTime이 필요하다.

```java
ZoneId zid = ZoneId.of("Asia/Seoul");
ZoneOffset krOffset = ZoneOffset.of("+9");

ZonedDateTime zdt = ZonedDateTime.of(date, time, zid);
OffsetDateTime odt = OffsetDateTime.of(date, time, krOffset);

// ZonedDateTime -> OffsetDateTime
OffsetDateTime odt = zdt.toOffsetDateTime();

```

### ZonedDateTime의 변환

ZonedDateTime도 LocalDateTime처럼 날짜와 시간에 관련된 다른 클래스로 변환하는 메서드를 가지고 있다.

```java
LocalDate toLocalDate()
LocalTime toLocalTime()
LocalDateTime toLocalDateTime()
OffsetDateTime toOffsetDateTime()
long toEpochSecond()
Instant toInstant()

// ZonedDateTime -> GregorianCalendar
GregorianCalendar from(ZonedDateTime zdt)

// GregorianCalendar -> ZonedDateTime
ZonedDateTime toZonedDateTime(
```

```java
package day12.time;

import java.time.*;

public class NewTimeEx2 {
	public static void main(String[] args) {
		LocalDate date = LocalDate.of(2021,  12, 31); // 2021년 12월 31일
		LocalTime time = LocalTime.of(12, 34, 56); // 12시 34분 56초
		
		// 2021년 12월 31일 12시 34분 56초
		LocalDateTime dt = LocalDateTime.of(date,  time);
		
		ZoneId zid = ZoneId.of("Asia/Seoul");
		ZonedDateTime zdt = dt.atZone(zid);
		//String strZid = zdt.getZone().getId();
		//System.out.println(strZid); // Asia/Seoul
		
		ZonedDateTime seoulTime = ZonedDateTime.now();
		ZoneId nyId = ZoneId.of("America/New_York");
		ZonedDateTime nyTime = ZonedDateTime.now().withZoneSameInstant(nyId);
		
		// ZonedDateTime -> OffsetDateTime
		OffsetDateTime odt = zdt.toOffsetDateTime();
		
		System.out.println(dt);
		System.out.println(zid);
		System.out.println(zdt);
		System.out.println(seoulTime);
		System.out.println(nyTime);
		System.out.println(odt);
	}
}

실행결과
2021-12-31T12:34:56
Asia/Seoul
2021-12-31T12:34:56+09:00[Asia/Seoul]
2022-05-05T19:40:28.799906600+09:00[Asia/Seoul]
2022-05-05T06:40:28.802895400-04:00[America/New_York]
2021-12-31T12:34:56+09:00
```

**time 클래스로 캘린더 만들기** 

```java
package exam01;

import java.time.*;
import java.util.Scanner;

public class Ex01 {
    public static void main(String[] args) {
        int year, month;

        Scanner scan = new Scanner(System.in);

        System.out.print("연도를 입력하세요 : ");
        year = scan.nextInt();

        System.out.print("월을 입력하세요 : ");
        month = scan.nextInt();

        LocalDate localDate = LocalDate.of(year, month, 1);
        System.out.println();
        System.out.printf("%d년 %d월 달력\n", year, month);
        System.out.printf("일\t월\t화\t수\t목\t금\t토\n");

        // 달의 마지막 날짜를 구함
        int lastOfDate = localDate.lengthOfMonth();
        // 지정한 달의 시작하는 요일을 구함
        int day = localDate.getDayOfWeek().getValue();
        //  만약 다른 연도나 월에서 첫 날짜가 일요일인 경우에도 동일한 문제가 발생할 것입니다.
        //따라서 이는 특정 월(예: 10월)에만 발생하는 문제가 아니라 코드의 로직 문제로, 모든 상황을 고려하지 않아 발생한 오류입니다.
        if (day == 7) {
            day = 0;
        }
        day++;

        // 달력 시작 날의 주말 처리
        for (int i = 1; i < day; i++) {
            System.out.print("\t");
        }

       int date = 1 ;
        for (int i = 0; i < lastOfDate; i++, date++) {
            System.out.printf("%d\t", date);

            if ( day %  7 == 0) {
                System.out.println();
            }
            day++;
        }
        scan.close();
    }
}
```

---

[참고하기](https://developer-talk.tistory.com/640)
[참고하기2](https://www.daleseo.com/java8-zoned-date-time/)
