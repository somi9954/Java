## 배열의 복사

: 배열은 한번 생성하면 그 길이를 변경할 수 없습니다. 따라서 더 많은 데이터를 저장하거나 기존의 배열과 똑같은 배열을 새로 만들려면 배열을 복사 해야한다. 복사 방법은 두가지가 있다.

- 얕은 복사(Shallow Copy): 복사된 배열이나 원본배열이 변경될 때 서로 간의 값이 함께 변경된다.

         '주소 값'을 복사한다는 의미한다.

![image](https://github.com/somi9954/Java/assets/137499604/089f68e7-ec16-4f2d-a781-7fa05cee73c2)


- 깊은 복사(Deep Copy): 복사된 배열이나 원본 배열이 변경될 때 서로 간의 값은 바뀌지 않는다.

         '실제 값'을 새로운 메모리 공간에 복사하는 것을 의미한다.

![image](https://github.com/somi9954/Java/assets/137499604/a16e8199-8b32-457f-a604-e70a201da190)


**얕은 복사**의 경우 주소 값을 복사하기 때문에, **참조하고 있는 실제값은 같습니다.**

### <1차원 배열의 복사>

- 얕은 복사

```java
package chap_06;

import java.util.Arrays;

public class ex04 {
    public static void main(String[] args) {

        int[] arr01 = {1, 2, 3};

        int[] arr02 = arr01; //배열의 얕은 복사, 배열과 같이 변수가 아닌 주소값을 가질땐 
				대입연산자는 값의 대입이 아닌 가지고 있는 값의 주소를 공유한다.

        System.out.println("arr01 배열 : " + Arrays.toString(arr01));

        arr02[1] = 10; //arr02 배열의 값 변경

				//arr01 변경 후 배열 출
        System.out.println("arr02 배열 : " + Arrays.toString(arr01));
        System.out.println("arr01 배열 : " + Arrays.toString(arr02));
    }
}
```

![image](https://github.com/somi9954/Java/assets/137499604/bae1b41a-999f-4b76-b5d6-c73c44fe4b56)


- 깊은 복사

```java

import java.util.Arrays;

public class ex04 {
    public static void main(String[] args) {

        int[] card = {3, 1, 4, 5, 10};

        int[] newcard = Arrays.copyOf(card, card.length); //. 배열의 깊은 복사 - Arrays.copyof(배열, 복사 범위)
        //newcard 배열에 card 배열의 길이만큼 복사. copyof 기능은 기존 배열의 위치가 아닌 새로운 배열을 생성한 후 반환

        System.out.println("card 배열 : " + Arrays.toString(card));

        card[1] = 10; //card 의 배열 값 변경

        //card 변경 후 배열 출력 => 한쪽이 변경되어도 영향을 받지 않는다.
        System.out.println("card 배열 :" + Arrays.toString(card));
        System.out.println("new card 배열 : " + Arrays.toString(newcard));

    }
}
```

![image](https://github.com/somi9954/Java/assets/137499604/1008b612-3b2a-45bb-a093-e4b7f7900f64)


### **배열을 복사하는 여러가지 메서드**

**Object.clone()**

```java
import java.util.Arrays;

public class ex08 {
    public static void main(String[] args) {
        int[] A = {10, 2, 30, 40};
        int[] B = A.clone();

        for (int num : B) {
            System.out.println(num);
        }

        System.out.println("B의 배열 : " + Arrays.toString(B));
     }
}
```

Array.clone()을 사용하면 배열을 쉽게 복사할 수 있습니다. (깊은 복사) 가장 보편적인 방법입니다.

**Arrays.copyOf()**

```java

import java.util.Arrays;

public class ex04 {
    public static void main(String[] args) {

        int[] card = {3, 1, 4, 5, 10};

        int[] newcard = Arrays.copyOf(card, card.length); //. 배열의 깊은 복사 - Arrays.copyof(배열, 복사 범위)
        //newcard 배열에 card 배열의 길이만큼 복사. copyof 기능은 기존 배열의 위치가 아닌 새로운 배열을 생성한 후 반환

        System.out.println("card 배열 : " + Arrays.toString(card));

        card[1] = 10; //card 의 배열 값 변경

        //card 변경 후 배열 출력 => 한쪽이 변경되어도 영향을 받지 않는다.
        System.out.println("card 배열 :" + Arrays.toString(card));
        System.out.println("new card 배열 : " + Arrays.toString(newcard));

```

Arrays클래스는 배열을 조작할 수 있는 메소드를 가진 클래스입니다. 이 클래스 안에 있는 Arrays.copyOf()를 사용하면 배열의 시작점 ~ 원하는 length까지 배열의 깊은 복사를 할 수 있습니다.

**Arrays.copyOfRange()**

```java
import java.util.Arrays;

public class ex07 {
    public static void main(String[] args) {

       int[] arr1 = {10, 20, 30, 40, 50};
        System.out.println();
        int[] arr3 = Arrays.copyOfRange(arr1, 0, 3);
	       //Arrays.copyOfRange(복사하고자하는 배열, 시작 위치, 배열크기);
				 // 특정범위를 지정해서 해당부분만 복사할 수 있다.
				1)for (int i = 0; i < arr3.length; i++) {
            System.out.println(arr3[i] + " ");
        }
        2)System.out.println("arr3의 배열 : " + Arrays.toString(arr3));
    }
}
```

Arrays.copyOf()는 배열의 처음~지정한 length까지 복사하는 메서드였다면 Arrays.copyOfRange() 메서드는 복사할 배열의 시작점도 지정할 수 있습니다.

**System.arraycopy()**

```java
import java.util.Arrays;

public class ex06 {
    public static void main(String[] args) {

        int[] card = {1, 6, 4, 5, 3, 2};
        int[] newcard = new int[card.length];

        System.arraycopy(card, 0, newcard,0,card.length);
        //         (복사 대상배열,복사시작위치,카피할 배열,시작 위치, 복사할 길이)

        System.out.println("card 배열 : " + Arrays.toString(card));
        System.out.println("newcard 배열 : " + Arrays.toString(newcard));
    }
}
```

System.arraycopy() 메서드는 지정된 배열을 대상 배열의 지정된 위치에 복사합니다.

### <2차원 배열의 복사>

- 얕은 복사

:  Object. clone()을 다차원 (2차원)배열에서 사용하면 얕은 복사가 된다. 아니면 반복문을 사용하여 복사를 할 수 있다.

```java
import java.util.Arrays;

public class ex09 {
    public static void main(String[] args) {
        int[][] A = {{1,3,5,7,9},{2,4,6,8,10}};

        int[][] B = A;
        int[][] C = A.clone();

        B[1][0] = 156;

        for (int i = 0; i <A.length ; i++) {
            System.out.println("A의 배열 : " + Arrays.toString(A[i]) +" ");
        }
        System.out.println();
        for (int i = 0; i < A.length; i++) {
            System.out.println("B의 배열 : " + Arrays.toString(B[i]) +" ");
        }
        System.out.println();
        C[0][1] = 248;
        for (int i = 0; i < A.length; i++) {
            System.out.println("C의 배열 : " + Arrays.toString(C[i]) +" ");
        }
    }
}
```

![image](https://github.com/somi9954/Java/assets/137499604/e3f7ba65-0a78-4d80-b660-0cf2dbccfb13)


2차원 배열의 경우, 위 결과처럼 clone을 했음에도 불구하고 변경된 값이 전부 적용 되버리는 것을 알 수 있다. 왜냐하면 객체들을 담고 있는 주소의 주소값 데이터를 새로 생성해 복사한 것이기 때문이다.

- 깊은 복사

: for문에 clone 같이 사용하는 방법, 2중 for문 사용을 사용하는 방법, 반복문 + System.arraycopy 방법 3가지가 있다.

1) for문에 clone 같이 사용하는 방법

```java
import java.util.Arrays;

public class ex10 {
    public static void main(String[] args) {

        int[][] arr1 = {{1,2},{3,4},{5,6}};
        int[][] arr2 = arr1;
        int[][] arr3 = arr1.clone();
        

       // 깊은 복사 (for문 + clone 사용)
		for(int i = 0; i < arr1.length ; i++) {
        arr3[i] = arr1[i].clone();

		arr1[2][0] = 10;

		for(int i = 0; i < arr1.length; i++) {
        System.out.print(Arrays.toString(arr1[i]) + " ");
          }
		System.out.println();

		for(int i = 0; i < arr2.length; i++) {
        System.out.print(Arrays.toString(arr2[i]) + " ");
         }
		System.out.println();

		for(int i = 0; i < arr3.length; i++) {
        System.out.print(Arrays.toString(arr3[i]) + " ");
          }
```

![image](https://github.com/somi9954/Java/assets/137499604/46571353-4ad3-4fe9-b363-507a6e7c27b1)


2) 2중 for문 사용을 사용하는 방법

```java
import java.util.Arrays;

public class ex10 {
    public static void main(String[] args) {

        int[][] arr1 = {{1,2},{3,4},{5,6}};
        int[][] arr2 = arr1;
	      int[][] arr4 = new int[3][2];

		// 깊은 복사 (2중 for문 사용)
		for(int i = 0; i < arr1.length; i++) {
        for(int j = 0; j < 2; j++) {
            arr4[i][j] = arr1[i][j];
         }
        }

        arr1[2][0] = 10;

		for(int i = 0; i < arr1.length; i++) {
        System.out.print(Arrays.toString(arr1[i]) + " ");
          }
		System.out.println();

		for(int i = 0; i < arr2.length; i++) {
        System.out.print(Arrays.toString(arr2[i]) + " ");
         }
		System.out.println();

    for(int i = 0; i < arr4.length; i++) {
        System.out.print(Arrays.toString(arr4[i]) + " ");
         }
   }
}
```

![image](https://github.com/somi9954/Java/assets/137499604/7cf1e339-275b-444e-a4bb-620523da6106)


3) 반복문 + System.arraycopy 방법

```java
import java.util.Arrays;

public class ex12 {
    public static void main(String[] args)  {
        int a[][] = {{1,2,3},{4,5,6,},{7,8,9}};
        int b[][] = new int[a.length][a[0].length];

        for(int i=0; i<a.length; i++){
            System.arraycopy(a[i], 0, b[i], 0, a[i].length);
						              //src, srcpos, dest, destpos,length
        }
        a[1][2] = 50;
        a[2][2] = 100;

        System.out.println("a : " + Arrays.deepToString(a));
        System.out.println("b : " + Arrays.deepToString(b));

    }
}
```

![image](https://github.com/somi9954/Java/assets/137499604/3638a2fc-259e-44e8-904c-853dee914618)

![image](https://github.com/somi9954/Java/assets/137499604/dcbc3841-da0f-49b1-b070-f51952629a16)
