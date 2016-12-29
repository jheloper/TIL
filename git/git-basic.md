# Git 정리

# 개념

- Git은 리누스 토발즈가 만든 버전 관리 시스템(Version Control System).
- 버전(Version)이란? 의미 있는 변화들 -> 기능의 개선, 또는 버그 수정, 요구 사항에 맞게 커스터마이징.
  - 버전 관리를 활용하고 있는 예: 위키피디아의 편집 히스토리.
  - 하나의 버전은 그 프로젝트의 저장소 안에서 모든 변경사항을 포함한다.
- 다른 버전 관리 시스템이 데이터를 다루는 방법은 각 파일의 변화를 시간순으로 관리하는 방법이며, Git이 데이터를 다루는 방법은 파일 시스템 스냅샷으로 관리하는 방법이다.
- Staging Area : 커밋 예정 대상들을 저장하는 공간.
- Staging Area의 존재 의미? 변경사항이 있는 파일들을 전체가 아닌 부분적으로 커밋할 수 있다.


## 파일의 상태
![git 파일 라이프사이클](./img/git-file-status.png)
- Untracked : 워킹 디렉터리에서 아직 스냅샷에 포함한 적이 없던 상태.
- Tracked : 워킹 디렉터리에서 이미 스냅샷에 포함되었던 상태.
- Unmodified : 이미 스냅샷에 포함되어 있지만 수정사항이 없는 상태.
- Modified : 스냅샷에 포함되어 있고 수정사항이 있는 상태.
- Staged : Staging Area에 포함된 상태.

# 로컬 저장소 만들기

`git init`

# 로컬 저장소 상태 확인

`git status`

`git status -s`

# Staging Area 추가(Add)

`git add <file>`

`git add --all`

git add 명령어는 Untracked 상태의 파일을 Staging Area에 추가할 때, 그리고 Tracked이면서 Modified 상태의 파일을 추가할 때도 사용한다.

주의할 점은 git add를 실행한 시점의 파일 상태가 Staging Area에 추가되기 때문에, 만약 git add를 한 후 또 수정사항이 생겼다면 해당 파일을 다시 git add 해주어야 최신 상태의 파일이 Staging Area에 들어간다.

# 커밋(Commit)

`git commit`

`git commit -m "Commit message."` : -m 플래그를 사용하여 커밋 메시지를 지정할 수 있다.

`git commit -a` : Tracked 상태의 파일을 Staging Area를 거치지 않고 바로 커밋.

# 태그

`git tag`

# 비교

`git diff`

# 커밋 히스토리 조회

`git log`

`git log --oneline`

# 되돌리기

`git commit --amend` : 바로 직전에 완료한 커밋에 현재 Staging Area 내용을 병합한다.

`git reset HEAD <file>` : Staging Area에 있는 파일을 Unstaged 상태로 바꾼다.

`git checkout -- <file>` : modified 상태의 파일을 Unmodified 상태로 바꾼다(수정 내용을 없애버린다).

# 삭제

`git rm <file>`

일반적인 파일 삭제와 git rm이 다른 점은, 일반적인 파일 삭제는 해당 파일을 Unstaged 상태로 만들어버릴 뿐이지만, git rm으로 삭제한 파일은 Staged 상태가 된다는 것이다. 이 차이는 커밋을 할 때 알 수 있는데, git rm으로 삭제한 파일은 삭제한 내용을 커밋하고 나서는 더 이상 해당 파일을 추적하지 않지만, 일반적으로 삭제한 파일은 커밋할 내용이 존재하지 않으며 git 디렉터리에는 Tracked 상태로 남는다는 점이다.

# 파일 이동

`git mv <from file> <to file>`

git mv 명령어는 파일의 이름을 바꾸는 데에도 사용할 수 있다.


# 브랜치(=Branch, 가지)

- 기본적으로 주어지는 브랜치의 이름은 master.
- 브랜치를 새로 생성하여 커밋하면 브랜치 생성 시점에서 분기점이 발생됨.
- 브랜치 간의 커밋은 독립적으로 이뤄진다.

## 브랜치 확인

`git branch`

## 브랜치 생성

`git branch <branch>`

`git checkout -b <branch>` : 브랜치를 생성함과 동시에 이동.

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

# Git 치트시트

![git 치트시트](./img/git-cheat-sheet.png)
