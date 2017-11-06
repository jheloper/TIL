# 자바 조건문과 반복문

# 조건문

## if 문

- 괄호 안에 들어갈 수 있는 것은 논리형 데이터(boolean 형)를 반환할 수 있는 어떠한 경우도 들어갈 수 있음.
- 명령문이 1줄이라면 중괄호 생략 가능(웬만하면 중괄호 사용할 것).
- 명령문이 2줄 이상이라면 중괄호 필요.
- if 문만 있다면 조건이 true인 경우에 실행, false인 경우는 실행하지 않고 건너뛴다.

## 중첩 if 문
- if 문 안에 또 다른 if 문이 있는 형태. 위의 if 값을 만족한 후에 실행된다. and라고 생각하면 될 듯.

## if ~ else 문
- if 문 조건이 true인 경우에는 if 문 안에 있는 명령을 실행하고, true가 아닌 경우에는 else문 안에 있는 명령을 실행.

## else if 문
- if 문 조건은 true가 아니지만, else if 문 조건에 true일 경우 실행할 명령을 지시. 모든 조건을 만족하지 않았다면, 건너뛰거나 else 문이 있으면 else 문의 내용을 실행한다. 이 경우 유의해야 할 점이 있는데, **실행 순서가 어디까지나 Top-Down 방식**이라는 점이다. 만약 특정 else if 문 조건에 충족하기 전에 다른 조건이 먼저 충족되었다면, 밑의 else if 문이나 else 문은 실행하지 않는다. 즉, 여러 케이스 중 하나를 만족하는 경우에 조건문의 처리 순서도 고려해야 한다.

## 조건문의 형태들
```java
// 조건식이 true면 execute(true).
if(true) {
    execute(true);
}

// 조건식이 true면 execute(true), 조건식이 false면 execute(false).
if(true) {
    execute(true);
} else {
    execute(false);
}

// 조건식 true1가 true이고 true2가 false이면 execute(true1),
// true1과 true2이 둘 다 true이면 execute(true1)을 실행한 후 execute(true2).
if(true1) {
     execute(true1);
     if(true2) {
          execute(true2);
     }
}

// 조건식 true1가 true이면 execute(true1), true1가 false이고 true2가 true이면 execute(true2),
// true1가 fasle이고 true2도 false, true3이 true이면 execute(true3), 조건식 모두 false면 execute(false).
if(true1) {
     execute(true1);
} else if(true2) {
     execute(true2);
} else if(true3) {
     execute(true3);
} else {
     execute(false);
}
```


## switch case 문
```java
switch(i){
    case 1:
        System.out.println("i is 1");
        break;
    case 2:
        System.out.println("i is 2");
        break;
    default:
        System.out.println("i is not 1 or 2");
        break;
}
```
- 정해진 몇가지의 case 중 하나를 골라야할 때.
- break 문은 case 실행 후 switch 문을 빠져나오는 역할을 한다.
- break 문이 없으면 break를 만날 때까지 계속 실행.
- switch case 문으로 코딩하더라도 자바 컴파일 시 자체적으로 if ~ else if 문으로 변환하여 컴파일한다. 이렇기에 속도 면에서 if ~ else if 문이 더 빠른 편이다.
- number, char, enum을 기준으로 제어하며, JDK 1.7 이후 문자열 제어가 추가되었다.

장점
- 코드의 가독성이 비교적 좋다.

단점
- switch에서 부등호 연산, 논리 연산 및 산술 연산이 불가능하다. 즉 정확한 값이 나오는 숫자나 글자 등을 사용해야 한다는 제약조건이 있다.
- break를 빼먹으면 다음 case까지 실행되어버린다. 컴파일 오류도 나지 않기에 코드 양이 많으면 찾아내기 힘든 경우도 있다.

# 반복문

## while 문
- 조건이 true인 동안 반복한다.
- 보통 초기식 >> 조건식 >> 명령문 >> 증감식 형태로 작성한다.

## do ~ while 문
- do 안에 있는 부분은 조건 만족 여부와 상관없이 반드시 한번은 실행한다.

## for 문
```java
for(int i = 0; i < 10; i++){
    System.out.println("hello");
}
```
- 조건식이 true이면 반복하고 증감식을 실행한 후 조건식을 다시 판단하여 반복 여부를 결정한다.
- (초기식; 조건식; 증감식)

## for each 문(=향상된 for 문)
```java
int arr[] = {1, 2, 3, 4, 5};
for(int item :arr){
    System.out.println(item);
}
```
- 배열에서 원소를 꺼내 for 문 안에서 사용한다.
- for 문과 성능 차이는 없다고 한다.

## 중첩 for 문
- for문 안에서 for문이 실행되는 것. 바깥 for 문의 조건식 결과가 true일 때 안쪽 for 문이 실행된다.
- 중첩 for문을 벗어날 때에는 라벨과 break문을 사용한다.
- 중첩 for문에서 continue 문을 사용할 때에도 라벨을 사용한다.

## break 문
- 반복문의 범위를 벗어나고 싶을 때 사용.

## continue 문
- 어떤 요소를 배제하고 실행하고 싶을 때 사용.

**중괄호를 사용하지 않아도 된다고 할지라도 되도록 중괄호를 사용해서 범위를 묶을 것.**
