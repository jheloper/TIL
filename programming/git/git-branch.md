# Git 브랜치

- 기본적으로 주어지는 브랜치의 이름은 master.
- 브랜치를 새로 생성하여 커밋하면 브랜치 생성 시점에서 분기점이 발생됨.
- 브랜치 간의 커밋은 독립적으로 이뤄진다.




## HEAD

- Git에 존재하는 특수한 포인터. 이 포인터는 현재 작업하는 로컬 브랜치를 가리킨다.




## 브랜치 확인

`git branch`

`git branch -v` : 브랜치마다 마지막 커밋 메시지도 함께 볼 수 있음.



## 브랜치 생성

`git branch <branch>` : 브랜치 생성.

`git checkout -b <branch>` : 브랜치를 생성함과 동시에 HEAD를 생성한 브랜치로 이동.



## 브랜치 이동

`git checkout <branch>`



## 브랜치 이름 변경

`git branch -m <branch old name> <branch new name>`



## 브랜치 삭제

`git branch -d <branch>`



## 브랜치 병합(Merge)

`git merge <branch>`

현재 브랜치와 대상 브랜치를 병합.



### 충돌(Conflict)의 예방 방법 및 최소화

오랜 기간 동안 서로 많은 양의 작업을 한 브랜치끼리 병합을 할 경우, 충돌을 피하기는 거의 불가능이다.

충돌을 최소회하기 위해서는, 특정 기간마다 다른 브랜치의 내용을 동기화해줄 필요가 있다.


