## **java.util.Scanner 클래스**

- Scanner는 화면, 파일, 문자열과 같은 입력소스로 부터 문자데이터를 읽어오는데 도움을 줄 목적으로 JDK1.5부터 추가되었다.
- Scanner에는 다음과 같은 생성자를 지원하기 때문에 다양한 입력소스로 부터 데이터를 읽을 수 있다.

```java
Scanner(String source)
Scanner(File source)
Scanner(InputStream source)
Scanner(Readable source)
Scanner(ReadableByteChannel source)
Scanner(Path source)

```

- 또한 Scanner는 정규식 표현(Regular expression)을 이용한 라인단위 검색을 지원하며 구분자(delimiter)에도 정규식 표현을 사용할 수 있어서 복잡한 형태의 구분자도 처리가 가능하다.

```java
Scanner useDelimiter(Pattern pattern)
Scanner useDelimiter(String pattern)

```

- 입력받을 값이 숫자라면 nextLine() 대신 nextInt() 또는 nextLong()과 같은 메서드를 사용할 수 있다.
- Scanner에서는 이와 같은 메서드를 제공함으로써 입력받은 문자를 다시 변환하는 수고를 덜어준다.

```java
boolean nextBoolean()  //boolean의 자료형, true,false로 대소문자를 구분하지 않는다.
byte nextByte()        //byte의 자료형
short nextShort()      //short의 자료형      
int nextInt()          //int형의 자료형
long nextLong()        //long형의 자료형
double nextDouble()    //double형의 자료형
float nextFloat()      //float형의 자료형
String next()          //String형의 문자열, 공백 문자를 기준으로 한 단어
String nextLine()      //String형의 문자열, 개행을 기준으로 한 줄
void close()           //Scanner 종료
boolean hasNext()      //boolean의 타입으로 반환되며 이동할 항목이 있다면 true을 리턴하고 그렇지 않으면 false을 리턴
```

**키보드 입력** 

Scanner는 InputStream을 생성자로 받을 수 있는데, 여기서 키보드 입력을 받으려면 System.in의 InputStream을 넘겨주면 됩니다.

```java
Scanner in=new Scanner(System.in);
```

```java
package day11.utils;

import java.util.*;

public class ScannerEx1 {
	public static void main(String[] args) {
		Scanner s = new Scanner(System.in);
		String[] argArr = null;

		while(true) {
			String prompt = ">>";
			System.out.print(prompt);

			// 화면으로부터 라인단위로 입력받는다.
			String input = s.nextLine();

			input = input.trim(); // 입력받은 값에서 불필요한 앞뒤 공백을 제거한다.
			argArr = input.split(" +"); // 입력받은 내용을 공백(1개 이상의) 으로 구분자로 자른다

			String command = argArr[0].trim();

			if ("".equals(command))
				continue;

			// 명령어를 소문자로 바꾼다.
			command = command.toLowerCase();

			// q또는 Q를 입력하면 실행종료한다.
			if (command.equals("q")) {
				System.exit(0);
			} else {
				for(int i = 0; i < argArr.length; i++) {
					System.out.println(argArr[i]);
				}
			}
		}
	}
}

```

![image](https://github.com/somi9954/Java/assets/137499604/f5a24a8b-ff44-4dc4-83f0-ec2a1404476f)

**파일에서 입력**

아래의 파일이 프로젝트와 같은 디렉토리에 존재한다.

![image](https://github.com/somi9954/Java/assets/137499604/06134d5d-a629-47c5-962c-0158bf1a84b6)

```java
package exam01;

import java.util.Scanner;
import java.io.File;
import java.io.IOException;

public class ScannerEx2 {
	public static void main(String[] args) throws IOException {
		Scanner sc = new Scanner(new File("data2.txt"));
		int sum = 0;
		int cnt = 0;
		
		while(sc.hasNextInt()) {
			sum += sc.nextInt();
			cnt++;
		}
		
		System.out.println("sum=" + sum);
		System.out.println("average=" + (double)sum/cnt);
	}
}

```

![image](https://github.com/somi9954/Java/assets/137499604/bcbaed86-f166-4964-9e2a-6b4230612343)
