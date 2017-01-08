# 객체 지향 프로그래밍(Object Oriented Programming, OOP)

객체(Object) = 클래스(Class) + 인스턴스(Instance).

클래스는 서로 연관되어 있는 데이터와 로직을 그룹화한 것.

인스턴스는 클래스를 통해 생성된 실체.

쉽게 생각하면 클래스는 하나의 틀, 그리고 인스턴스는 클래스라는 틀을 이용해서 만든 실체라고 생각할 수 있다.

앞으로 클래스나 인스턴스의 **멤버**는 *변수와 메서드를 포함해서 부르는 것으로 정의*한다.

# 클래스 정의
```python
class User(object):
    def __init__(self):
        ......
```



# 인스턴스 생성
`user = User()`

내부적으로 생성자 메서드가 호출된다.



# 클래스 생성자 메서드
`__init__`



# 인스턴스 멤버
```python
class User:
    def __init__(self, name):
        self.name = name

    def get_name(self):
        return self.name

user = User()
user.get_name() # 인스턴스 메서드 호출.
```
## 인스턴스 메서드
클래스 내부에 선언된 함수가 인스턴스 메서드가 된다. 인스턴스 메서드는 첫번째 파라미터로 반드시 인스턴스 자신(self)을 받는다.

## 인스턴스 변수
인스턴스 메서드 내에서 `self.변수명`으로 접근한다. 따로 명시적으로 선언할 필요는 없다.



# 클래스 멤버
## 클래스 메서드
인스턴스를 통하지 않고 클래스를 통해서 사용할 수 있는 메서드. 첫번째 파라미터로 클래스 자신(cls)을 받는다.

`@classmethod` 데코레이터를 통해서 선언한다.

```python
class User:
    @classmethod
    def class_method(cls):
        print("Class method...")

User.class_method() #클래스 메소드 호출...
```

## 클래스 변수

클래스 변수는 클래스가 공유하는 변수다. 따라서 클래스를 사용해서 만든 인스턴스들은 클래스 변수를 함께 공유한다.

클래스의 내부이면서 메소드의 밖에 선언한 변수는 클래스 변수이다.

클래스 변수에 접근할 때에는 `클래스명.변수명`으로 접근한다.

```python
class User:
    count = 0
    def __init__(self):
        User.count = User.count + 1
    @classmethod
    def getCount(cls):
        return User.count

user1 = User()
user2 = User()
user3 = User()
user4 = User()
print(User.getCount())
```


# 정적(Static) 메서드
인스턴스가 아닌 클래스에서 바로 사용하는 메서드. 클래스 메서드와의 차이는 클래스 내부에 접근할 수 없다는 점이다. 독립된 일반 함수와 유사하다고 볼 수 있다.

`@staticmethod` 데코레이터를 통해서 선언한다.

```python
class User:
    @staticmethod
    def static_method():
        print("Static method...")

User.static_method() #클래스의 static 메소드 호출...
```


# 캡슐화
파이썬에서는 인스턴스 변수에 직접 접근할 수 없도록 인스턴스 변수에 접두어로 접근제어자를 지정할 수 있음.

`self.__변수명`
