# 자바 추상 클래스

## 추상 클래스

객체를 직접 생성할 수 있는 클래스를 실체 클래스라고 한다면 이 클래스들의 공통적인 특성을 추출해서 선언한 클래스를 추상 클래스라고 함. 추상 클래스와 실체 클래스는 상속의 관계를 가지고 있음. 추상 클래스가 부모이고 실체 클래스가 자식으로 구현되어 실체 클래스는 추상 클래스의 모든 특성을 물려받고, 추가적은 특성을 가질 수 있음.

추상 클래스는 실체 클래스의 공통되는 필드와 메서드를 추출해서 만들었기 때문에 객체를 직접 생성해서 사용할 수 없음.

추상 클래스는 새로운 실체 클래스를 만들기 위해 부모 클래스로만 사용됨.



## 추상 클래스의 용도

### 실체 클래스들의 공통된 필드와 메서드의 이름을 통일하기 위한 목적

실체 클래스의 설계자가 여러 사람일 경우, 실체 클래스마다 필드와 메서드가 제각기 다른 이름을 가질 수 있음. 따라서 필드와 메서드의 이름의 통일성을 위해 사용하기도 함.

### 실체 클래스 작성 시 시간 절약

공통적인 필드와 메서드를 추상 클래스에 선언해두고, 실체 클래스마다 다른 점만 실체 클래스에 선언하게 되면 실체 클래스를 작성하는데 시간을 절약할 수 있음.



## 추상 클래스 선언

```java
public abstract class 클래스 {}
```

`abstract` 키워드를 사용하여 추상 클래스를 선언함.

new 연산자로 직접 생성자를 호출할 수는 없지만 자식 객체가 생성될 때 `super()`를 호출하므로 추상 클래스도 생성자가 필요함.



## 추상 메서드와 오버라이딩

추상 클래스는 실체 클래스가 공통적으로 가져야 할 필드와 메서드들을 정의해 놓은 클래스이므로 실체 클래스의 멤버를 통일화하는데 목적이 있음.

메서드의 선언만 통일화하고, 실행 내용은 실체 클래스마다 달라야 하는 경우가 있는데, 이런 경우를 위해 추상 클래스는 추상 메서드를 선언할 수 있음.

추상 메서드는 추상 클래스에서만 선언할 수 있는데, 메서드의 선언부만 있고 메서드 실행 내용인 중괄호 {}가 없는 메서드를 말함.

자식 클래스는 반드시 추상 메서드를 오버라이딩해서 실행 내용을 작성해야 함.

```java
[public | protected] abstract 리턴타입 메서드명(매개변수, ...);
```