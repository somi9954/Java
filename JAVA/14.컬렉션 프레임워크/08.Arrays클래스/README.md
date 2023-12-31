# Arrays클래스

- 배열을 다루는데 유용한 메서드가 정의되어 있다.
- 같은 기능의 메서드가 배열의 타입만 다르게 오버로딩되어 있어서 많아 보이지만 실제로 그렇지는 않다.
- Arrays 클래스의 메소드는 다음과 같다.

| 분류 | 메서드 명 | return type | 설명 |
| --- | --- | --- | --- |
| 배열 변환 | Arrays.asList(array) | List<T> | 해당 메서드는 배열(Array)을 기반으로 Collection 함수의 ArrayList로 형변환을 하여 반환해주는 함수입니다. |
| 배열 복사 | Arrays.copyOf(array, copyArrayLenght) | T[] | 해당 메서드는 배열 전체를 복사하여서 복사할 길이 만큼 지정하여 복사한 새로운 배열로 반환해주는 함수입니다. |
| 배열 복사 | Arrays.copyOfRange(array, startIntex, endIndex) | T[] | 해당 메서드는 원본 배열의 시작 인덱스와 끝 인덱스를 지정하여서 복사한 새로운 배열로 반환해주는 함수입니다. |
| 배열 채우기 | Arrays.fill(array, n) | void | 해당 메서드는 배열내에 지정한 범위 내에 “동일한 값”으로 채워주는 함수입니다. |
| 배열 채우기 | Arrays.setAll(array, generator) | void | 해당 메서드는 배열을 채우는데 사용하는 배열이며, 배열의 값은 순차적으로 메서드로 “구성한 값”으로 채워주는 함수입니다. |
| 배열 값 출력 | Arrays.toString(array) | String | 해당 메서드는 배열을 문자열로 변환하여 반환해주는 함수입니다. |
| 배열 정렬 | Arrays.sort(array) | void | 해당 메서드는 배열내의 요소들을 오름차순/내림차순, 특정 구간을 정하여 정렬을 수행해주는 함수입니다. |
| 배열 간의 비교 | Arrays.equals(array1, array2); | boolean | 해당 메서드는 두 배열이 “동일한 수”의 요소를 포함하고 두 배열이 모든 해당 “요소 쌍의 값이 동일한지”에 대해 비교하여 진위형(boolean)으로 반환해주는 함수입니다. |
| 배열 간의 비교 | Arrays.deepEquals(array1, array2) | boolean | 해당 메서드는 단일 차원 또는 다차원 배열의 두 배열이 같은지 여부를 비교하여 진위형(boolean)으로 반환해주는 함수입니다. 또한 차원에 관계없이 두 개의 중첩 배열(즉, 다차원 배열)을 비교할 수 있습니다. |
| 배열 요소 검색 | Arrays.binarySearch() | int (index) | 해당 메서드는 배열의 요소를 검색하여 해당 요소의 인덱스를 반환해주는 함수입니다. |

### **Arrays.copyOf(array, copyArrLength)**

> 💡 해당 메서드는
> 
> 
> **배열 전체를 복사하여서 복사할 길이만큼 지정하여 복사한 새로운 배열로 반환해 주는 함수**
> 

```java
int[] arr = {0, 1, 2, 3, 4};

// 동일한 배열을 복사합니다.
int[] newArray1 = Arrays.copyOf(arr, arr.length);// [0, 1, 2, 3, 4]
int[] newArray2 = Arrays.copyOf(arr, 3);// [0, 1, 2]
int[] newArray3 = Arrays.copyOf(arr, arr.length + 3);// [0, 1, 2, 3, 4, 0, 0, 0]
```

### **Arrays.copyOfRange(array, startIntex, endIndex)**

> 💡 해당 메서드는
> 
> 
> **원본 배열의 시작 인덱스와 끝 인덱스를 지정하여서 복사한 새로운 배열로 반환해 주는 함수**
> 

```java
int[] arr = {0, 1, 2, 3, 4};
int[] copyArrIdx = Arrays.copyOfRange(arr, 0, arr.length + 2);// [0, 1, 2, 3, 4, 0, 0]
```

| 분류 | Arrays.CopyOf() | Arrays.copyOfRange |
| --- | --- | --- |
| 복사 시작 인덱스 지정 가능 여부 | O | O |
| 복사 끝 인덱스 지정 가능 여부 | X | O |
| 복사 사이즈 초과시 값 채워줌 여부 | O | O |

### **Arrays.fill(array, value) / Arrays.fill(array, startIndex, endIndex, value)**

> 💡 해당 메서드는
> 
> 
> **배열 내에 지정한 범위 내에 “동일한 값”으로 채워주는 함수**
> 

```java
/*
 * Arrays.fill : 해당 메서드는 배열내에 지정한 동일한 값으로 채워주는 함수입니다.
 */// [CASE1] 모든 빈 공간에 채워주는 fillint[] fillArr1 = new int[5];
Arrays.fill(fillArr1, 369);// [369, 369, 369, 369, 369]// [CASE2] 2,3,4 공간에 해당 값을 채워주는것과 같지만 모두 다 채워준다.int[] fillArr2 = new int[5];
fillArr2[0] = 123;
fillArr2[1] = 456;
fillArr2[2] = 789;
Arrays.fill(fillArr2, 369);// [369, 369, 369, 369, 369]// [CASE3] 특정 구간에 채워주는 방식 (시작 인덱스와 종료인덱스 입력)int[] fillArr3 = new int[5];
fillArr3[0] = 123;
fillArr3[1] = 456;
fillArr3[2] = 689;
Arrays.fill(fillArr3, 3, fillArr3.length, 369);// [123, 456, 689, 369, 369]// [CASE4] fill 함수와 repeat 함수를 사용하여 순차적인 별 채워넣기
String[] fillArr4 = new String[5];
for (int i = 0; i < fillArr4.length; i++) {
    Arrays.fill(fillArr4, i, i + 1, "*".repeat(i + 1));// "*", "**", "***", "****", "*****"
}

// [CASE5] 배열의 길이보다 더 채워주는 경우 => 에러 발생 : Array index out of range: 8int[] fillArr5 = new int[5];
fillArr5[0] = 123;
fillArr5[1] = 456;
fillArr5[2] = 689;
Arrays.fill(fillArr5, 3, fillArr5.length + 3, 369);// Array index out of range: 8
```

### **Arrays.setAll(array, generator)**

> 💡 해당 메서드는
> 
> 
> **배열을 채우는 데 사용하는 배열이며, 배열의 값은 순차적으로 메서드로 “구성한 값”으로 채워주는 함수**
> 

```java
// [CASE1] setAll을 통해 배열 내에 변형된 숫자를 채워넣는다. : 100까지 랜덤한 숫자들로 배열을 채워 넣는다
int[] arr1 = new int[5];
  Arrays.setAll(arr1, i -> (int) (Math.random() * 101);// 64, 17, 69, 56, 6// 

[CASE2] setALL을 통해 배열 내에 변형된 문자을 채워 넣는다. : 별을 순차적으로 증가시켜 배열에 추가를 합니다.
  String[] arr2 = new String[5];
  Arrays.setAll(arr2, i -> "*".repeat(i + 1));// ["*", "**", "***", "****", "*****"]
```

| 분류 | Arrays.fill() | Arrays.setAll() |
| --- | --- | --- |
| 변형 데이터의 반영 가능 여부 | X | O |

### **Arrays.sort(array)**

> 💡 해당 메서드는
> 
> 
> **배열 내의 요소들을 오름차순/내림차순, 특정 구간을 정하여 정렬을 수행해 주는 함수**
> 

**1. 숫자 배열의 정렬**

```java
/*
 * 숫자 배열의 정렬
 */
Integer[] sortNumArr1 = {0, 1, 2, 3, 4};
Integer[] sortNumArr2 = {10, 11, 1, 2, 4};

// [CASE1] 숫자 오름차순 정렬 -1 : 오름차순으로 정렬이 됩니다.
Arrays.sort(sortNumArr1);// [0, 1, 2, 3, 4]
Arrays.sort(sortNumArr2);// [1, 2, 4, 10, 11]// [CASE2] 숫자 오름차순 정렬 -2 : 오름차순으로 정렬이 됩니다.
Arrays.sort(sortNumArr1, Comparator.naturalOrder());// [0, 1, 2, 3, 4]
Arrays.sort(sortNumArr2, Comparator.naturalOrder());// [1, 2, 4, 10, 11]// [CASE3] 숫자 내림차순 정렬 -1 : 내림차순으로 정렬이 됩니다.(* 해당 주의 사항은 Wrapper Class 를 이용하여야 합니다.)
Arrays.sort(sortNumArr1, Collections.reverseOrder());// [4, 3, 2, 1, 0]
Arrays.sort(sortNumArr2, Collections.reverseOrder());// [11, 10, 4, 2, 1]// [CASE4] 숫자 내림차순 정렬 -2 : 내림차순으로 정렬이 됩니다.(* 해당 주의 사항은 Wrapper
Arrays.sort(sortNumArr1, Comparator.reverseOrder());// [4, 3, 2, 1, 0]
Arrays.sort(sortNumArr2, Comparator.reverseOrder());// [11, 10, 4, 2, 1]// [CASE5] 숫자 인덱스 범위 정렬 : 시작 인덱스와 종료 인덱스를 선택하여서 정렬이 됩니다.
Arrays.sort(sortNumArr1, 0, 3);// [1, 10, 11, 2, 4]

Integer[] sortNumArr3 = {10, 11, 1, 2, 4};

// [CASE5] 숫자 내림차순 정렬 : Lambda를 이용한 내림 차순으로 정렬
Arrays.sort(sortNumArr3, (s1, s2) -> s2 - s1);// [11, 10, 4, 2, 1]// [CASE6] 숫자 오름차순 정렬 : Lambda를 이용한 오름 차순으로 정렬
Arrays.sort(sortNumArr3, (s1, s2) -> s1 - s2);// [1, 2, 4, 10, 11]
```

**2. 문자열 배열의 정렬 : 대소문자 구분하여 정렬**

```java
/*
 * 문자열의 정렬-1 : 대소문자를 구분하여 정렬하는 방식
 */
String[] sortStrArr1 = {"strawberry", "Strawberry", "mango", "Mango", "cherry", "Cherry", "banana", "Banana", "apple", "Apple"};

// [CASE1] 문자 정렬 : 오름차순으로 정렬합니다.
Arrays.sort(sortStrArr1);// [Apple, Banana, Cherry, Mango, Strawberry, apple, banana, cherry, mango, strawberry]// [CASE2] 문자 정렬 : 내림차순으로 정렬이 됩니다. (* 해당 주의 사항은 Wrapper Class 를 이용하여야 합니다.)
Arrays.sort(sortStrArr1, Collections.reverseOrder());// [strawberry, mango, cherry, banana, apple, Strawberry, Mango, Cherry, Banana, Apple]
```

**3. 문자열 배열의 정렬 : 대소문자 구분 없이 정렬**

```java
/*
 * 문자열의 정렬-2 : 대소문자 구분없이 정렬하는 방식
 */
String[] sortStrArr2 = {"strawberry", "Strawberry", "mango", "Mango", "cherry", "Cherry", "banana", "Banana", "apple", "Apple"};

// [CASE1] 문자 정렬 : 오름차순으로 정렬합니다. : 대소문자 구분 O
Arrays.sort(sortStrArr2, String.CASE_INSENSITIVE_ORDER);// [apple, Apple, banana, Banana, cherry, Cherry, mango, Mango, strawberry, Strawberry]// [CASE2] 문자 정렬 : 내림차순으로 정렬합니다. : 대소문자 구분 O
Arrays.sort(sortStrArr2, Collections.reverseOrder(String.CASE_INSENSITIVE_ORDER));// [strawberry, Strawberry, mango, Mango, cherry, Cherry, banana, Banana, apple, Apple]
```

### **Arrays.binarySearch()**

> 💡 해당 메서드는
> 
> 
> **배열의 요소를 검색하여 해당 요소의 인덱스를 반환해주는 함수**
> 

binarySearch() 메소드의 기능은 정렬이 되어있는 배열을 가지고 있다고 가정할 때

그 배열에서 매개변수로 넣은 값이 이미 존재하는지 여부와 그와 동시에 만약 있다면

이 배열의 index번호상으로 몇번에 위치하는지, 이미 존재하지 않는다면 이 배열의

정렬된 현재 상태와 비교하여 매개변수로 넣은 값이 배열에 추가되었다고 가정할 때

이 배열에서 몇번째 순서로 위치할지 알 수 있도록 하는 기능을 가지고 있다.

```java
Arrays.binarySearch(배열변수, 검색할 값); -- 반환타입 int

ex) int a[] = {1, 3, 5, 7, 9}; <- 이런 배열이 있다고 가정한다
		int index = Arrays.binarySearch(a, 3);
    index 는 1의 값을 가지게 된다.

    int index = Arrays.binarySearch(a, 10);
    index 는 -6의 값을 가지게 된다.
```

![image](https://github.com/somi9954/Java/assets/137499604/ee076566-89ce-46ad-86fe-036d7da166d0)

위의 그림과 같이 해당 값이 존재하면 해당 값의 인덱스 값을그렇지 않으면 위의 그림과 같이 1부터 시작하는 인덱스 값으로 반환하고, 부호는 음수로 하여 표현하게 된다.

그리고 음수로 표현이 되는 경우, 인덱스번호 0번 앞에 위치하면 -1을 인덱스번호 1번 앞에 위치하게 되면 -2를 반환하게 된다.

어떠한 상황이든 배열에는 인덱스 번호를 가지게 되고 때문에반환되는 정수값은 이 배열의 인덱스번호를 상대적인 개념으로값들을 비교하여 위치값을 int형태로 반환하는 것이다.

binarySearch() 메소드의 매개변수가 다른  즉 오버로드된메소드의 종류는 상당히 많은편이다. 하지만 기본동작의 형식은 위에서 설명한 대로 작동하니 이점만 잘 파악하면 문제가 없을 것이다

### **Arrays.equals(array1, array2) : 1차원 배열**

> 💡 해당 메서드는
> 
> 
> **두 배열이 “동일한 수”의 요소를 포함하고 두 배열이 모든 해당 “요소 쌍의 값이 동일한지”에 대해 비교하여 진위형(boolean)으로 반환해 주는 함수**
> 

```java
/*
 * Arrays.equals : 해당 메서드는 두 배열이 동일한 수의 요소를 포함하고 두 배열이 모든 해당 요소 쌍이 동일한지에 대한 비교를 수행합니다.
 */
int[] arr1 = {1, 2, 3, 4};
int[] arr2 = {1, 2, 3, 4};
int[] arr3 = {1, 2, 4, 3};

boolean isEquals1 = Arrays.equals(arr1, arr2);// trueboolean isEquals2 = Arrays.equals(arr1, arr3);// false
```

### **Arrays.deepEquals(array1, array2) : 단일 차원 또는 다차원 배열**

> 💡 해당 메서드는
> 
> 
> **단일 차원 또는 다차원 배열의 두 배열이 같은지 여부를 비교하여 진위형(boolean)으로 반환해 주는 함수입니다.**
> 

```java
int a1[][] = {{10, 20}, {40, 50}, {60, 70}};
int a2[][] = {{30, 20}, {10, 0}, {60, 80}};
int a3[][] = {{10, 20}, {40, 50}, {60, 70}};

boolean isDeepEquals1 = Arrays.deepEquals(a1, a2);// falseboolean isDeepEquals2 = Arrays.deepEquals(a1, a3);// true
```

| 분류 | Arrays.equals() | Arrays.deepEquals() |
| --- | --- | --- |
| 1차원 배열 비교 여부 | O | O |
| 다차원 배열 비교 여부 | X | O |

### **Arrays.toString(array)**

> 💡 해당 메서드는
> 
> 
> **배열을 문자열로 변환하여 반환해 주는 함수**
> 

```java
/*
 * Arrays.toString : 해당 메서드는 배열을 문자열로 변환해주는 함수입니다.
 */
int[] orgArr = {0, 1, 2, 3, 4};// [0, 1, 2, 3, 4]String arrToStr = Arrays.toString(arr);// "[0, 1, 2, 3, 4]",
```

### **Arrays.asList(array): 배열 변환**

> 💡 해당 메서드는 배열(Array)을 기반으로 Collection 함수의
> 
> 
> **ArrayList로 형변환을 하여 반환해 주는 함수입니다**
> 

```java
// 1. [배열 -> 컬렉션 함수] 배열(Array) 선언 및 초기화합니다.
String[] strArr = {"one", "two", "three"};

// 2. [배열 -> 컬렉션 함수] 배열 리스트(ArrayList) 선언 및 초기화합니다.
List<String> strArrList = new ArrayList<>(Arrays.asList(strArr));    
// ArrayList : ["one", "two", "three"]

// 1. [컬렉션 함수 -> 배열]  배열(Array) 사이즈 지정합니다.
String[] strArr2 = new String[strArrList.size()];

// 2. [컬렉션 함수 -> 배열] 배열(Array) - 배열리스트 값을 전환합니다.
strArr2 = strArrList.toArray(strArr2);                              
// String[] : ["one", "two", "three"]

```
