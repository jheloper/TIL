# 개요

도커(Docker)는 컨테이너 기반 기술.

가상머신과 컨테이너의 차이점?
가상머신은 게스트 OS를 설치해야 한다. 그래서 가상머신의 이미지는 용량이 크고 성능도 떨어지기 마련이다.
컨테이너는 게스트 OS를 설치하지 않고, OS 자원을 호스트와 공유한다. 애플리케이션과 라이브러리만을 격리하여 가상화하므로, 비교적 용량이 작고 성능 손실이 적다.

원래 도커는 리눅스의 LXC 기술을 기반으로 하였으나, 현재는 libcontainer라는 독자적인 기술을 사용한다.

![가상머신 구조](./img/docker-vm.png)
![도커 구조](./img/docker-docker.png)

## 장점
1. 용량이 적다.
2. 성능에 영향이 적다.
3. 이식성이 뛰어나다.

## 단점
1. 리눅스 커널에 종속적이기에 윈도우나 맥의 경우 리눅스 가상머신이 필요하다.

## 이미지와 컨테이너
- 베이스 이미지 : 리눅스 배포판의 유저랜드(userland)만 설치된 파일.
- 도커 이미지 : 베이스 이미지 + 애플리케이션 환경 기반.
- 컨테이너 : 이미지를 실제로 실행시킨 상태의 인스턴스.



# 기본 사용법
## 도커 이미지 검색
```docker
docker search [검색키워드]
```
[Dockerhub](https://hub.docker.com/)에서 이미지를 검색한다.

## 이미지 받기
```docker
docker pull [이미지명:태그]
```
공식 이미지는 이미지명 앞에 아무것도 붙이지 않지만, 사용자 이미지의 경우 이미지명 앞에 `사용자명/`을 붙인다.

## 이미지 목록 조회
```docker
docker images
docker images [이미지명]
```
다운로드 받거나 생성한 이미지 목록을 조회한다. 이미지명을 붙이면 해당 이미지명으로 조회한다.

## 컨테이너 생성
```docker
docker create [옵션] [이미지명] [명령]
docker create -i -t -p 80:80 --name [컨테이너명] /bin/bash
```
컨테이너를 생성한다.

`-i, -t, --name, -p, -e, -v` 등의 옵션을 자주 사용한다.

## 컨테이너 생성과 동시에 시작
```docker
docker run [옵션] [이미지명] [명령]
docker run -i -t --name [컨테이너명] /bin/bash
docker run -d -p 80:80 --name [컨테이너명] /bin/bash
```
컨테이너를 생성과 동시에 시작한다.

`-i, -t, --name, -p, -e, -d, -v` 등의 옵션을 자주 사용한다.

## 컨테이너 목록 조회
```docker
docker ps
docker ps -a
```
현재 실행중인 컨테이너 목록 조회. `-a` 옵션을 사용하면 현재 정지 상태인 컨테이너까지 모두 조회한다.

## 컨테이너 시작 및 재시작, 정지
```docker
docker start [컨테이너명]
docker restart [컨테이너명]
docker stop [컨테이너명]
```

## 컨테이너 접근
```docker
docker attach [컨테이너명]
```
bash 셸에서 `exit`, 또는 `ctrl+d` 를 입력하면 컨테이너 정지. `ctrl+p`, `ctrl+q`를 누르면 컨테이너 정지하지 않고 빠져나오기.

## 컨테이너 내부 명령 실행
```docker
docker exec [컨테이너명] [명령]
docker exec [컨테이너명] echo "Hello World!"
```

## 컨테이너 및 이미지 삭제
```docker
docker rm [컨테이너명]
docker rmi [이미지명:태그]
```

## 컨테이너 변경사항 비교
```docker
docker diff [컨테이너명]
```

## 컨테이너 세부사항 조회
```docker
docker inspect [컨테이너명]
```

## 이미지 히스토리 조회
```docker
docker history [이미지명:태그]
```
