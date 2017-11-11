# Git 기본 사용법



## 로컬 저장소 만들기

`git init`



## 로컬 저장소 상태 확인

`git status`

`git status -s`



## Staging Area 추가(Add)

`git add <file>`

`git add --all`

`git add` 명령어는 Untracked 상태의 파일을 Staging Area에 추가할 때, 그리고 Tracked이면서 Modified 상태의 파일을 추가할 때도 사용한다.

주의할 점은 `git add`를 실행한 시점의 파일 상태가 Staging Area에 추가되기 때문에, 만약 `git add`를 한 후 또 수정사항이 생겼다면 해당 파일을 다시 `git add` 해주어야 최신 상태의 파일이 Staging Area에 들어간다.



## 커밋(Commit)

`git commit`

`git commit -m "Commit message."` : -m 플래그를 사용하여 커밋 메시지를 지정할 수 있다.

`git commit -a` : Tracked 상태의 파일을 Staging Area를 거치지 않고 바로 커밋.



## 태그

`git tag`



## 비교

`git diff`



## 커밋 히스토리 조회

`git log`

`git log --oneline`



## 되돌리기

`git commit --amend` : 바로 직전에 완료한 커밋에 현재 Staging Area 내용을 병합한다.

`git reset HEAD <file>` : Staging Area에 있는 파일을 Unstaged 상태로 바꾼다.

`git checkout -- <file>` : modified 상태의 파일을 Unmodified 상태로 바꾼다(수정 내용을 없애버린다).



## 삭제

`git rm <file>`

일반적인 파일 삭제와 `git rm`이 다른 점은, 일반적인 파일 삭제는 해당 파일을 Unstaged 상태로 만들어버릴 뿐이지만, `git rm`으로 삭제한 파일은 Staged 상태가 된다는 것이다. 이 차이는 커밋을 할 때 알 수 있는데, `git rm`으로 삭제한 파일은 삭제한 내용을 커밋하고 나서는 더 이상 해당 파일을 추적하지 않지만, 일반적으로 삭제한 파일은 커밋할 내용이 존재하지 않으며 git 디렉터리에는 Tracked 상태로 남는다는 점이다.



## 파일 이동

`git mv <from file> <to file>`

git mv 명령어는 파일의 이름을 바꾸는 데에도 사용할 수 있다.



## Git 치트시트

![git 치트시트](./img/git-cheat-sheet.png)
