# 자바 중첩 클래스와 중첩 인터페이스

## 중첩 클래스와 중첩 인터페이스

클래스가 여러 클래스와 관계 맺을 경우 독립적으로 선언하는 것이 좋으나, 특정 클래스와 관계 맺을 경우 관계 클래스를 클래스 내부에 선언하는 것이 좋음.

중첩 클래스(nested class)는 클래스 내부에 선언한 클래스를 의미하며, 중첩 클래스를 사용하면 두 클래스의 멤버들을 서로 쉽게 접근할 수 있다는 장점과 외부에는 불필요한 관계 클래스를 감춤으로써 코드의 복잡성을 줄일 수 있음.

인터페이스 역시 클래스 내부에 선언 가능. 이런 인터페이스를 중첩 인터페이스라고 하며, 특정 클래스와 긴밀한 관계를 갖는 구현 클래스를 생성하기 위해서 사용함.

```java
class OuterClass {
    class NestedClass {
        ...
    }
    interface NestedInterface {
        ...
    }
}
```



## 중첩 클래스

클래스 내부에 선언되는 위치에 따라 2가지로 분류됨.

- 멤버 클래스 : 클래스의 멤버로서 선언되는 중첩 클래스.
- 로컬 클래스 : 메서드 내부에서 선언되는 중첩 클래스.

멤버 클래스는 클래스나 객체가 사용 중이라면 언제든지 재사용 가능, 허나 로컬 클래스는 메서드 실행 시에만 사용되고 메서드 실행 종료 후 없어짐.

### 인스턴스 멤버 클래스(Instance Member Class)

`static` 키워드 없이 선언된 멤버 클래스. 인스턴스 멤버 클래스는 인스턴스 필드와 메서드만 선언 가능하고 정적 필드와 메서드는 선언 불가함.

### 정적 멤버 클래스(Static Member Class)

`static` 키워드로 선언된 멤버 클래스. 정적 멤버 클래스는 모든 종류의 필드와 메서드를 선언할 수 있음.

### 로컬 클래스(Local Class)

메서드 내에서 선언된 중첩 클래스. 로컬 클래스는 접근 제한자 및 `static`을 붙일 수 없음. 메서드 내부에서만 사용되므로 접근 제한이 불필요하기 때문. 로컬 클래스에는 인스턴스 필드와 메서드만 선언 가능하며 정적 필드와 메서드는 선언 불가함.



## 중첩 클래스의 접근 제한

### 바깥 필드와 메서드에서 사용 제한

멤버 클래스가 인스턴스 또는 정적으로 선언됨에 따라 바깥 클래스의 필드와 메서드에 사용 제한이 생김.

인스턴스 멤버 클래스는 바깥 클래스의 인스턴스 필드나 인스턴스 메서드에서 객체를 생성할 수 있으나, 정적 필드나 정적 메서드에서는 객체를 생성할 수 없음. 반면 정적 멤버 클래스는 모든 필드나 메서드에서 객체 생성이 가능함.

### 멤버 클래스에서 사용 제한

멤버 클래스가 인스턴스 또는 정적으로 선언됨에 따라 멤버 클래스 내부에서 바깥 클래스의 필드와 메서드를 접근할 때에도 제한이 생김.

인스턴스 멤버 클래스 안에서는 바깥 클래스의 모든 필드와 메서드에 접근할 수 있으나 정적 멤버 클래스 안에서는 바깥 클래스의 정적 필드와 메서드에만 접근 가능함.

### 로컬 클래스에서 사용 제한

로컬 클래스 내부에서는 바깥 클래스의 필드나 메서드를 제한없이 사용할 수 있음. 허나 메서드의 매개변수나 로컬 변수를 로컬 클래스에서 사용할 때, 메서드 실행이 끝나면 매개변수나 로컬 변수가 스택 메모리에서 사라지기 때문에 문제가 발생함. 자바는 이 문제를 해결하기 위해 컴파일 시 로컬 클래스에서 사용하는 매개변수나 로컬 변수의 기억 장소를 로컬 클래스 내부에 복사해서 사용함. 그리고 매개변수나 로컬 변수가 수정되어 기억장소가 변경되면 로컬 클래스에 복사해 둔 기억장소와 달라지는 문제를 해결하기 위해 매개변수나 로컬 변수를 `final`로 선언해서 수정을 방지함.

결론적으로 로컬 클래스에서 사용 가능한 것은 `final`로 선언된 매개변수와 로컬 변수뿐이라는 것. 자바 8부터는 `final` 키워드 없이 선언된 매개변수와 로컬 변수의 사용이 가능해졌는데, 이것은 사실 내부적으로 `final`로 선언하지 않은 매개변수와 로컬 변수를 로컬 클래스에서 사용할 경우 로컬 클래스의 필드로 복사되는 것임.

### 중첩 클래스에서 바깥 클래스 참조 얻기

클래스 내부에서 `this`는 객체 자신의 참조. 중첩 클래스에서 `this` 키워드를 사용하면 바깥 클래스의 객체 참조가 아니라 중첩 클래스의 객체 참조가 됨. 중첩 클래스 내부에서 바깥 클래스의 객체 참조를 얻으려면 바깥 클래스 이름을 `this` 앞에 붙여줘야 함.

```java
OuterClass.this.field;
OuterClass.this.method();
```



## 중첩 인터페이스

중첩 인터페이스는 클래스의 멤버로 선언된 인터페이스. 인터페이스를 클래스 내부에 선언하는 이유는 해당 클래스와 긴밀한 관계를 맺는 구현 클래스를 만들기 위해서임.

아래와 같이 중첩 인터페이스를 클래스 내부에 선언한 후,

```java
public class Button {
    ClickListener listener;
    
    void setClickListener(ClickListener listener) {
        this.listener = listener;
    }
    
    void click() {
        listener.click();
    }
    
    interface ClickListener {
        void click();
    }
}
```

다음과 같이 `외부클래스.중첩인터페이스명`으로 구현 클래스를 만들고,

```java
public class CallListener implements Button.ClickListener {
    @Override
    public void click() {
        System.out.println("Click the Call Button!");
    }
}
```

```java
public class MessageListener implements Button.ClickListener {
    @Override
    public void click() {
        System.out.println("Click the Message Button!");
    }
}
```

다음과 같이 구현 클래스의 객체를 생성해서 사용할 수 있음.

```java
public class Main {
    public static void main(String[] args) {
        Button button = new Button();
        
        button.setClickListener(new CallListener);
        button.click();
        
        button.setClickListener(new MessageListener);
        button.click();
    }
}
```