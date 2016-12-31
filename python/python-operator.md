# 연산자
- 타 언어(예를 들면 C언어나 자바 등...)의 연산자와 많은 부분이 비슷함.
- 특이한 점이라고 할 수 있는 것 중 하나는 문자열에 대한 multiply 연산이 가능함. -> `'hello' * 3 == 'hellohellohello'`
- 논리연산은 `is, and, or, not` 키워드를 사용함.

# 산술 연산자
```python
1 + 2    # 3
3 - 1    # 2
2 * 4    # 8
5 / 2    # 2.5
5 % 2    # 1 (Modular 연산, 몫이 아닌 나머지를 구함)
5 ** 3   # 125 (제곱 연산, 5의 3제곱을 뜻함)
5 // 2   # 2 (몫을 구할 때 소수점 이하를 버림)
```

# 비교 연산자
`>, >=, <, <=, ==, !=`

# 논리 연산자

단독으로 쓰이는 경우는 거의 없고 주로 조건문에서 사용.
```python
a = 10
if a is 10:
    print('a is 10')

if not a is 1:
    print('a is not 1.')

if a > 5 and a < 11:
    print('a is more than 5, and less than 11.')

if a < 15 or a < 8:
    print('a is less than 15, or less than 8.')
```

# 비트 연산자

파이썬에서 `&, |` 연산자는 비트 연산자이다. 여기에 더하여 `<<, >>, ~, ^` 비트 연산자가 있다.
