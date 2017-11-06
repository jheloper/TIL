# 파이썬 데코레이터

데코레이터(Decorator)? 기존에 정의된 함수에 기능을 추가하거나 확장할 때 사용한다. 어떤 작업의 전후에 수행할 공통 로직을 관리하기 위해 사용하여 코드의 재사용성과 관심사의 분리를 효과적으로 적용할 수 있다.

```python
def func_decorator(func):
    def decorate():
        print('before')
        func()
        print('after')
    return decorate()

@func_decorator
def sum(x, y):
    print(x + y)
```
위의 코드와 같이 데코레이터 함수를 정의하고, 데코레이터를 사용하고자 할 때에는 `@`에 데코레이터 이름을 붙여서 사용한다.

위와 같이 데코레이터를 함수로 정의할 수도 있지만, 클래스로 정의하는 것도 가능하다. `__call__` 메서드로 정의해주면 된다.

```python
class FuncDecorator:
    def __init__(self, func):
        self.func = func

    def __call__(self, *args, **kwargs):
        print('before')
        self.func(*args, **kwargs)
        print('after')

class MyClass:
    @FuncDecorator
    def sum(self, x, y):
        print(x, y)
```
