# 함수
- def 키워드로 선언.
- 함수 시그너처는 `def 함수명(파라미터)`이다.
```python
def func(param1):
    print(param1)
    return True
```
- 파이썬의 함수는 객체이다. 따라서 변수에 할당할 수 있으며, 다른 함수의 파라미터로 넘길 수도 있다.
- 변수에 함수를 할당할 때, 실행하고 할당하면 반환 값이 할당되지만 실행하지 않고 할당하면 함수 객체가 할당된다.


# 내부함수
- 함수 안에 함수를 선언할 수 있다.
```python
def func1():
    def func2():
        return 1 + 2
    print(func2())
```


# 내장함수
수가 꽤 많으므로 자세한 내용은 [링크 참조](https://docs.python.org/3/library/functions.html)
- print()
- input()
- len()
- range()
- enumerate()
- open()
