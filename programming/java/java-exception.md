# 자바 예외(Exception)
자바에서 오류(error)와 예외(exception)는 다름. 오류는 하드웨어의 오동작 또는 고장으로 프로그램 실행 오류가 발생하는 것. 반면 예외는 잘못된 조작 또는 개발로 인해 발생하는 프로그램 오류를 의미함. 예외 처리를 통해 예외가 발생해도 프로그램을 종료하지 않고 실행 상태가 유지되도록 할 수 있음.

예외를 크게 2종류로 나누자면, **일반 예외(Exception)**와 **실행 예외(Runtime Exception)**으로 나눌 수 있음. 일반 예외는 컴파일러 체크 예외라고도 하는데, 소스 컴파일 과정에서 예외 처리가 필요한지 검사하기 때문. 실행 예외는 컴파일 과정에서 예외 처리를 검사하지 않는 예외를 말함.

자바에서는 예외를 클래스로 관리함. 예외 클래스의 종류는 매우 많다. [자바 공식 문서](https://docs.oracle.com/javase/8/docs/api/)의 Exception 클래스 항목을 참조할 것.

모든 예외 클래스는 `java.lang.Exception` 클래스를 상속받음.

Exception 클래스를 상속받고 RuntimeException 클래스를 상속받지 않는 클래스는 일반 예외 클래스, RuntimeException 클래스를 상속받는 클래스는 실행 예외 클래스로 구별함.



## 실행 예외(Runtime Exception)

실행 예외는 컴파일러가 체크하지 않기 때문에 개발자의 경험에 의해 예외 처리 코드를 삽입해야 함. 만약 개발자가 실행 예외에 대해 예외 처리를 하지 않았을 경우, 해당 예외 발생 시 프로그램은 종료됨.

아래는 자주 발생하는 실행 예외들.

### NullPointerException

객체 참조가 없는 상태, null 값을 갖는 참조 변수로 객체 접근 연산자인 `.`를 사용했을 때 발생함. 즉, 객체가 없는 상태에서 객체를 사용하려 했을 때 발생하는 것.

### ArrayIndexOutOfBoundsException

배열에서 인덱스 범위를 초과하여 접근할 경우 발생함.

### NumberFormatException

래퍼 클래스의 `parseXXX()` (예를 들면 `Integer.parseInt()`) 메서드를 사용하면 문자열을 숫자로 변환할 수 있는데, 숫자로 변환할 수 없는 문자가 메서드의 매개변수에 포함되어 있으면 발생함.

### ClassCastException

형변환이 불가능한 경우인데도 형변환을 시도할 경우 발생. 형변환 전에 `instanceof` 연산자로 확인하면 예방할 수 있음.



## 예외 처리

### try-catch-finally

try 블록 안에 예외 발생 가능 코드를 위치시키고, catch 블록 안에는 예외 발생 시 실행할 코드를 위치시킴. finally 블록 안에는 예외 발생 여부와 상관없이 무조건 실행해야 하는 코드가 위치함.

finally 블록은 생략 가능함.

try 블록, catch 블록에서 return 문을 사용하더라도 finally 블록은 항상 실행됨.

```java
try {
    예외 발생 가능 코드
} catch (예외클래스 e) {
    예외 발생 시 실행할 코드
} finally {
    무조건 실행함, 후처리 영역. 생략 가능함.
}
```
### 다중 catch

try 블록 안에서 여러 종류의 예외가 발생할 수 있을 때, 발생되는 예외 별로 예외 처리 코드를 다르게 하려면 다중 catch 블록을 사용해야 함.

```java
try {
    Test1Exception, 또는 Test2Exception이 발생할 수 있음.
} catch (Test1Exception e) {
    Test1Exception 발생 시 예외 처리.
} catch (Test2Exception e) {
    Test2Exception 발생 시 예외 처리.
}
```

여러 catch 블록 중 하나만 실행되는데, 그 이유는 try 블록에서 동시다발적으로 예외가 발생하지 않고 하나의 예외가 발생하면 즉시 실행을 멈추고 해당 catch 블록으로 이동하기 때문임.

다중 catch 블록 작성 시 주의점은 *상위 예외 클래스가 하위 예외 클래스보다 아래쪽에 위치해야 한다*는 점. try 블록에서 예외 발생 시 예외 처리할 catch 블록은 위에서부터 차례대로 검색되는데, 만약 상위 예외 클래스의 catch 블록이 위에 있다면 하위 예외 클래스의 catch 블록은 실행되지 않음. 하위 예외 클래스는 상위 예외 클래스를 상속했기 때문에 상위 예외 타입으로도 취급할 수 있기 때문임.

### 멀티 catch

자바 7부터 하나의 catch 블록에서 여러 예외를 처리할 수 있도록 멀티 catch 기능을 추가함. catch 괄호() 안에 동일하게 처리하고 싶은 예외를 `|`로 연결.

```java
try {
    Test1Exception, 또는 Test2Exception이 발생할 수 있음.
   	다른 Exception이 발생할 수 있음.
} catch(Test1Exception | Test2Exception e) {
    Test1Exception 또는 Test2Exception 발생 시 예외 처리.
} catch(Exception e) {
    다른 Exception 발생 시 예외 처리.
}
```

### try-with-resources

자바 7에서 추가됨. 예외 발생 여부와 상관없이 사용했던 리소스 객체의 `close()` 메서드를 호출해서 안전하게 리소스를 닫을 수 있음. 복수 개의 리소스를 사용하는 것도 가능함.

```java
try(
    FileInputStream fis = new FileInputStream("test1.txt");
    FileOutputStream fos = new FileOutputStream("test2.txt")
) {
    ...
} catch(IOException e) {
    ...
}
```

try 블록에서 예외가 발생하면 우선 리소스를 닫고 catch 블록을 실행함. 다만 리소스 객체가 `java.lang.AutoCloseable` 인터페이스를 구현하고 있어야 함.



## 예외 떠넘기기

### throws

메서드 선언부 끝에 `throws` 키워드를 붙이며 메서드에서 처리하지 않은 예외를 호출한 곳으로 떠넘김.

`throws` 키워드가 있는 메서드는 try 블록 내에서 호출되어야 하고 catch 블록에서 예외를 처리해야 함.

생성자에도 `throws` 키워드를 붙일 수 있음.

```java
public void someMethod() throws Test1Exception, Test2Exception, ... {
    ...
}
```

`main()` 메서드에서도 `throws` 키워드를 사용해서 예외를 떠넘길 수 있는데, JVM이 최종적으로 예외 처리를 하게 됨. JVM은 예외 내용을 콘솔에 출력하는 것으로 예외 처리함. 허나 `main()` 메서드에 `throws`를 사용하는 것은 권장하지 않음. 프로그램이 예외 내용을 출력하고 종료되기 때문.

### throw

`throw` 키워드를 사용하면 의도적으로 예외를 발생시킬 수 있음.

예외 메시지가 필요하면 예외 메시지를 갖는 생성자를 이용하면 됨.

```java
throw new Exception();
throw new Exception("message");
```

예외 발생 코드를 가지고 있는 메서드는 내부에서 try-catch 블록으로 예외 처리할 수 있으나, 대부분은 자신을 호출한 곳에서 예외 처리하도록 `throws` 키워드로 예외를 떠넘김.



## 사용자 정의 예외

자바 표준 API에서 여러 예외 클래스를 제공하고 있으나 부족한 경우 필요한 예외 클래스를 직접 정의할 수 있음.

`Exception` 클래스(실행 예외인 경우에는 `RuntimeException` 클래스)를 상속해서 예외 클래스를 정의하면 됨.

```java
public class TestException extends Exception {
    public TestException(){}
    public TestException(String message) { super(message); }
}
```

사용자 정의 예외 클래스도 필드, 생성자, 메서드를 선언할 수 있으나 대부분의 경우 생성자 선언만 포함함. 생성자는 2개를 선언하는 것이 일반적이며 하나는 기본 생성자, 하나는 예외 메시지를 전달하기 위해 String 타입 매개변수를 갖는 생성자로 선언함.

