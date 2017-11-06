# PHP 함수
PHP의 함수는 기본적으로 전역 함수. 

호출하기 전에 정의할 필요가 없다. 이것의 의미는 호출하는 부분이 코드 상에서 먼저 나오고 정의하는 부분이 이후에 나온다고 하더라도 문제 없이 호출된다는 의미이다.

함수 오버로딩은 지원하지 않는다. 함수 정의를 해제하거나 정의된 함수를 재정의할 수 없다.
```php
// 함수 정의
function func($param) {
    echo 'this is function.';
    echo "param is {$param}";
    return true;
}

// 함수 호출
func(3);
```

## 함수의 조건적 정의
함수를 조건적으로 정의할 경우에는 반드시 함수 정의가 호출보다 먼저 위치해야 한다.
```php
if ($i === 1) {
    function func1() {
        return $i;
    }
}

// 또 다른 코드들...

// 함수를 조건적으로 정의할 경우 동일한 조건을 체크해주고 호출하는 것이 안전한 방법이다. 
if ($i === 1) {
    func1();
}
```

## 내부 함수
함수 내부에 함수를 정의하는 "내부 함수" 사용이 가능하다. PHP의 내부 함수는 외부 함수와 같은 범위를 가지기 때문에 내부 함수를 외부에서 호출할 수 있다.
```php
function outerFunc() {
    function innerFunc() {
        echo 'this is inner function.';
    }
}
// 외부 함수를 먼저 호출해야 내부 함수를 호출할 수 있다.
outerFunc();
// 내부 함수를 외부에서도 호출할 수 있다.
innerFunc();
```

## 재귀 함수
```php
function recursion($i) {
    if($i < 10) {
        recursion($i + 1);
    } else {
        echo $i;
    }
}
```


# 함수 인자

PHP의 함수 인자는 기본적으로 값에 의한 전달(passing by value)이다.

## 참조 인자 전달하기

```php
$a = 'abc';

function func(&$param) {
    $param = 123;
}

func($a);
echo $a; // 123
```

## 인자 기본값 지정하기

인자 기본값으로는 4가지 스칼라형뿐 아니라 `array`와 `null`도 사용할 수 있다.

인자 기본값을 지정할 때에는 기본값을 쓰지 않는 인자가 왼쪽, 기본값을 지정한 인자가 오른쪽에 위치해야 한다.

```php
function func($param = 'this is default value') {
    echo $param;
}

func(null); // 'this is default value'
func('this is parameter'); // 'this is parameter'
```

## 함수 반환값

함수의 반환값은 배열이나 객체를 포함하여 모든 타입이 가능하다. return 키워드를 만나면 함수의 수행이 즉시 중단되고 현재 함수를 호출한 곳으로 제어권을 돌려준다.

반환값은 여러 개가 될 수 없으나, 배열로 반환하는 방법을 사용할 수 있다.

```php
function func() {
    return array(1, 2, 3);
}
```

