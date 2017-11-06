# PHP 조건문과 반복문

# 조건문

## if문(+elseif, else)
```php
if(exp1) {
    // exp1이 true이면 실행.
} elseif(exp2) {
    // exp1이 false, exp2이 true이면 실행.
} else {
    // exp1도, exp2도 false이면 실행.
}
```

## switch-case문
```php
switch($i) {
    case 1:
        // $i이 1이면...
        break;
    case 2:
        // $i이 2이면...
        break;
    default:
        // $i이 어느 조건에도 해당하지 않으면...
        break;
}
```


# 반복문
## for문
```php
for ($i = 0; $i < 10; $i++) {
    echo $i;
}
```

## foreach문
```php
$arr = [
    'foo' => '1',
    'bar' => '2',
];
foreach($arr as $key => $value) {
    echo $key . ' : ' . $value;
}
```

## while문
```php
while (exp) {
    // exp가 true이면 반복.
}
```

## do while문
```php
do {
    // 기본적으로 while문과 동일하나, 첫 반복은 무조건 실행한다는 점이 다르다.
    // 선 실행 후 조건 판단.
} while (exp);
```