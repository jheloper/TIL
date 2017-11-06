# Docker mariadb container 생성(i386 CPU, 우분투 14.04 기준)

보유중인 구형 서버의 CPU 아키텍처가 i386이기 때문에 i386 CPU 기준 방법을 작성한다.

[mariadb ubuntu repository link](https://downloads.mariadb.org/mariadb/repositories/#mirror=kaist&distro=Ubuntu&distro_release=trusty--ubuntu_trusty&version=10.1)

```bash
sudo apt-get install software-properties-common
sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xcbcb082a1bb943db
sudo add-apt-repository 'deb [arch=amd64,i386,ppc64el] http://ftp.kaist.ac.kr/mariadb/repo/10.1/ubuntu trusty main'
sudo apt-get update
sudo apt-get install mariadb-server
```

