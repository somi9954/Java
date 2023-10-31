## object 클래스란?

: 모든 클래스 상속계층도의 최상위에 있는 조상 클래스이다. 다른 클래스로부터 상속 받지 않은 모든 클래스들은 자동적으로 Object  클래스로부터 상속 받게 함으로써 이것을 가능하게 한다. 

Object 클래스에는 다양한 메소드가 존재하는데, 어떤 클래스에서도 호출할 수 있다.

- Object클래스 대표 메소드 종류

      - equals() 메소드 : 두 객체가 동일한 객체라면 true를 리턴하고, 다르다면 false를 리턴합니다.
      - hashCode() 메소드 : 객체의 메모리 번지를 이용해서 해시코드를 만들어서 리턴한다. 객체마다 다른 값을 가     지고있다.

      - toString()메소드 : 객체의 문자 정보를 리턴한다. 즉 객체를 문자열로 표현한다. 

      - final Class<?> **getClass( ) :**  현재 객체의 클래스 정보를 담은 Class타입의 객체를 반환합니다.

      - protected Object **clone( ) :** 현재 객체의 복사본을 생성후 반환합니다. (Cloneable 인터페이스를 구현한 클래스만 복사 가능함)

      - final void **notify() :** 현재 객체를 사용하기 위해 대기하고 있는 쓰레드 하나를 깨웁니다.

      - final void **notifyAll() :** 현재 객체를 사용하기 위해 대기하고 있는 모든 쓰레드를 깨웁니다.

      - final void **wait() :**  다른 쓰레드가 깨울때까지 현재 쓰레드를 대기시킵니다.

      -final void **wait(long timeoutMillis) :** 다른 쓰레드가 깨우거나 정해진 시간만큼 현재 쓰레드를 대기시킵니다.

      -final void **wait(long timeoutMillis, int nanos) :** 다른 쓰레드가 깨우거나 정해진 시간만큼 현재 쓰레드를 대기시킵니다.

       -protected void **finalize( ) :** 객체가 소멸되기 전 자동으로 호출되는 메소드로, 현재는 Deprecated 되어 사용하지 않습니다. (삭제예정)

### Object 클래스 예시

```java
public class ExampleClass {
    private int exampleField;

    public ExampleClass(int exampleField) {
        this.exampleField = exampleField;
    }

    public int getExampleField() {
        return exampleField;
    }

    public void setExampleField(int exampleField) {
        this.exampleField = exampleField;
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        ExampleClass that = (ExampleClass) o;
        return exampleField == that.exampleField;
    }

    @Override
    public int hashCode() {
        return Objects.hash(exampleField);
    }

    @Override
    public String toString() {
        return "ExampleClass{" +
                "exampleField=" + exampleField +
                '}';
    }
}

```

위의 예시 클래스에서 볼 수 있듯이, 모든 클래스는 Object 클래스를 상속 받게 된다. 이를 통해 다른 클래스와의 호환성을 유지하면서, 모든 객체는 Object 클래스의 메소드를 호출할 수 있다.
