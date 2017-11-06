# PHP 타입
- 4가지 스칼라형 : boolean, integer, float, string
- 2가지 복합형 : array, object
- 3가지 특수형 : resource, null, callable


# 변수
php의 변수는 `$`로 시작한다.
```php
$var1 = 'this is variable.'
```

`$this`는 특수 변수로, 할당이 불가능하다.

## 변수 유효범위
```php
// 전역 유효범위
$var1 = 'this is global scope.'
function func(){
    // 지역 유효범위
    $var1 = 'this is local scope.'
}
```

## 참조에 의한 지정
`&` 참조 연산자를 사용하여 특정 변수의 참조를 지정할 수 있다.
```php
$var = 'abc';
$foo = &$var;
$foo = 123;
# $var의 값이 123으로 변경됨.
```


# Boolean
참과 거짓 값을 나타낸다. true, false로 표현하며 대소문자를 가리지 않으나 소문자로 표현하는 것을 PSR에서 권장하고 있다.
다음과 같은 값은 연산자, 함수, 조건문에서 자동으로 false 값으로 변환된다.

- boolean FALSE
- integer 0 (zero)
- float 0.0 (zero)
- 비어있는 string, 그리고 string "0"
- 요소를 가지지 않는 array
- 멤버 변수를 가지지 않는 object (PHP 4 에서만 적용)
- 특별한 타입 NULL (unset 변수 포함)
- 빈 태그로부터 만들어진 SimpleXML 객체

이외의 값은 true로 간주된다.

여기서 유의할 것은, 정수 -1 역시 true로 간주된다는 것이다. 즉, 위의 false로 간주되는 값이 아닌 모든 값은 true라고 생각하면 된다.

# String
PHP의 문자열은 작은 따옴표, 큰 따옴표 모두 사용이 가능하지만 약간의 기능적 차이가 존재한다.
- 작은 따옴표(single quote)의 경우, 단순한 문자열을 나타내는 데에 사용한다.
- 큰 따옴표(double quote)의 경우, 변수를 문자열에 포함시킬 수 있으며 몇 가지 이스케이프 문자(\n, \r, \t 등...)를 지원한다.

```php
$singleQuoteStr = 'this is single quote.';
# 'this is single quote.'
$one = 1;
$doubleQuoteStr = "$one\nthis is double quote.";
# '1
# this is double quote.'
```

# Array
PHP의 배열은 연관 배열까지 포함된다.

## 선언 및 할당
```php
$arr = array(1, 2, 3, 4);
$arr = [1, 2, 3, 4]
$map = array(
    'key1' => 'foo',
    'key2' => 'bar',
)
$map = [
    'key1' => 'foo',
    'key2' => 'bar',
]
```

## 요소 삽입, 삭제
```php
$arr = array();
$arr[] = 1;
unset($arr[0]);
```
php 배열에 요소를 삽입할 때에는 위와 같은 방식으로 삽입한다. 또한 특정 요소를 삭제할 때에도 위와 같이 하면 된다. 다만 `unset()`을 통해 요소를 삭제할 때에 요소를 판별할 수 있는 키 값이나 인덱스가 필요하다.


# Object
PHP 역시 객체 타입이 존재한다.

## 객체 선언 및 생성, 멤버 접근
```php
class cls {
    # member variable
    public $var;

    # method
    public function func() {
        return true;
    }
}

$foo = new cls();
$foo->var;
$foo->func();
```

# 상수
PHP에서 상수는 `define()` 함수를 사용하거나 `const` 키워드를 사용하여 정의한다.
```php
# define 함수를 이용한 상수 선언. 이후 TEN으로 접근할 수 있다.
define('TEN', 10);
# const 키워드를 이용한 상수 선언.
const ONE = 1;
```

## 마법 상수(미리 정의된 상수)
```php
# 파일의 현재 줄 번호
__LINE__;
# 심볼릭 링크를 통해 해석된 경우를 포함한 파일의 전체 경로와 이름. include 내부에서 사용할 경우, include된 파일명이 반환.
__FILE__;
# 파일의 디렉터리. 포함한 파일 안에서는, 포함된 파일의 디렉터리를 반환. 이는 dirname(__FILE__)과 동일하다. 디렉터리 이름은 루트 디렉터리가 아닌 이상, 마지막에 슬래시(/)를 포함하지 않는다.
__DIR__;
# 함수 이름.
__FUNCTION__;
# 클래스 이름. 네임스페이스를 포함한다.
__CLASS__;
# 클래스 메서드 이름.
__METHOD__;
# 현재 네임스페이스 이름.
__NAMESPACE__;
```