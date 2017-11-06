
# 기본 사용법


## 도커 이미지 검색

```shell
docker search [검색키워드]
```
[Dockerhub](https://hub.docker.com/) 또는 [Docker Store](https://store.docker.com)에서 이미지를 검색한다.



## 이미지 받기

```shell
docker pull [이미지명:태그]
```
공식 이미지는 이미지명 앞에 아무것도 붙이지 않지만, 사용자 이미지의 경우 이미지명 앞에 `사용자명/`을 붙인다.



## 이미지 목록 조회

```shell
docker images
docker images [이미지명]
```
다운로드 받거나 생성한 이미지 목록을 조회한다. 이미지명을 붙이면 해당 이미지명으로 조회한다.



## 컨테이너 생성

```shell
docker create [옵션] [이미지명] [명령]
docker create -i -t -p 80:80 --name [컨테이너명] /bin/bash
```
컨테이너를 생성한다.

`-i, -t, --name, -p, -e, -v` 등의 옵션을 자주 사용한다.



## 컨테이너 생성과 동시에 시작

```shell
docker run [옵션] [이미지명] [명령]
docker run -i -t --name [컨테이너명] /bin/bash
docker run -d -p 80:80 --name [컨테이너명] /bin/bash
```
컨테이너를 생성과 동시에 시작한다.

`-i, -t, --name, -p, -e, -d, -v` 등의 옵션을 자주 사용한다.



## 컨테이너 목록 조회

```shell
docker ps
docker ps -a
```
현재 실행중인 컨테이너 목록 조회. `-a` 옵션을 사용하면 현재 정지 상태인 컨테이너까지 모두 조회한다.



## 컨테이너 시작 및 재시작, 정지

```shell
docker start [컨테이너명]
docker restart [컨테이너명]
docker stop [컨테이너명]
```



## 컨테이너 접근

```bash
docker attach [컨테이너명]
```
bash 셸에서 `exit`, 또는 `ctrl+d` 를 입력하면 컨테이너 정지. `ctrl+p`, `ctrl+q`를 누르면 컨테이너 정지하지 않고 빠져나오기.



## 컨테이너 내부 명령 실행

```shell
docker exec [컨테이너명] [명령]
docker exec [컨테이너명] echo "Hello World!"
```



## 컨테이너 및 이미지 삭제

```shell
docker rm [컨테이너명]
docker rmi [이미지명:태그]
```



## 컨테이너 변경사항 비교

```shell
docker diff [컨테이너명]
```



## 컨테이너 세부사항 조회

```shell
docker inspect [컨테이너명]
```



## 이미지 히스토리 조회

```shell
docker history [이미지명:태그]
```

