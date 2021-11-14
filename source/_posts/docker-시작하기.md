---
title: docker 시작하기
date: 2021-04-04 00:44:40
tags:
    - Docker
categories:
    - Docker
---

### docker 설치

-   도커 설치 : https://www.docker.com/get-started
-   docker desktop을 설치
-   powershell에서 도커 버전 확인 : docker --version

---

### docker 설치 시 주의사항

-   windows에서 설치할 경우 WSL 2와 관련된 설정이 나올 텐데 이를 허용해야 한다.

---

### 실습 환경 설정

-   git clone https://gitlab.com/yalco/practice-docker.git DokerStudy
-   Node.js : 브라우저가 아닌 컴퓨터 환경에서 자바스크립트를 돌리게 해줌

---

### 실습 코드 수행

-   npm install --global http-server : global로 설치를 해야 http-server 명령어 이용 가능합니다.
-   cd frontend로 들어간 후 http-server -p 8080 ./public 명령으로 서버 실행

-   그러나 이러한 Node.js와 http-server 없이 실행하기 위해 도커를 사용한다.

---

### docker 실행

-   docker run -it node : 만약 permission 관련 오류 발생 시 sudo를 붙이면 됨
-   Node.js 깔린 것처럼 입력 콘솔이 출력된다
-   이 Node.js 환경은 이미지 형태인데, docker의 이미지란 것은 캡쳐해서 박제한 것이다

#### docker 설명

-   run은 다운 후 이미지를 해동해서 컨테이너로 만든다
-   -it는 컨테이너를 연 다음 cli를 사용하겠다는 의미이다
-   그 후 node 명령어가 실행되므로 입력 화면이 나오는 것이다

#### docker 조작하기

-   docker images : 설치 된 것 확인, 설치 되었으니 docker run -it node 명령어 사용하면 설치없이 바로 실행
-   docker ps : 컨테이너 확인 가능
-   docker exec -it (docker ps 명령어로 확인한 컨테이너 명) bash
-   root@f44956de125d:/# 가 뜨면서 컨테이너 내부를 통해 가상의 리눅스 환경으로 들어간 것이다
-   ls를 입력하면 리눅스 기본 디렉터리들이 보인다 -> 컨테이너마다 각각 이 파일 시스템과 네트워크가 존재, 도커 데스크탑 프로그램으로 구현된 것!!!
-   도커의 컨테이너들은 리눅스 가상 환경의 형태로 돌아감!

#### docker 종료하기

-   node cli에서 ctrl+c를 하면 컨테이너 안의 Node와 회의를 끝마친 것이다
-   이 후 docker ps를 입력하더라도 컨테이너가 나타나지 않는다
-   docker ps -a : 모든 컨테이너를 보여줌, 현재 중지된 컨테이너도 보임

-   이 디렉터리에서만 확인할 수 있는 것이 아니라 docker에 의해 다른 곳에서 관리 되므로 어떠한 디렉터리에서도 확인이 가능

#### docker container 삭제

-   한번에 도커 컨테이너 삭제
-   docker stop $(docker ps -aq)
-   docker system pune -a

---

### Dockerfile

-   이미지를 만들기 위한 설계서

#### Dockerfile 내용

-   FROM node:12.18.4 : node version
-   RUN npm install -g http-server : 이미지를 생성할 과정에서 실행할 명령어
-   WORKDIR /home/node/app : 이 안에서 명령어를 수행할 위치
-   CMD ["http-server", "-p", "8080", "./public"] : 이미지로부터 컨테이너가 만들어져 가동될 때 기본적으로 바로 실행되는 명령어

#### Dockerfile 실행

-   cli에서 이 폴더로 들어온 다음 -t 뒤에 원하는 이미지명을 적은 뒤 Docker file로의 상대 경로를 적는다
-   파일이 Dockerfile이면 따로 명시할 필요가 없음
-   docker build -t frontend-img .
-   docker images 명령어를 통하여 node 이미지가 다운 받아지고 이를 기반으로 frontend-img 이미지가 만들어진다

#### image run 시키기

-   docker run --name frontend-con -v $(pwd):/home/node/app -p 8080:8080 frontend-img
-   docker run --name frontend-con -v "%cd%":/home/node/app -p 8080:8080 frontend-img
-   아까는 도커가 임의의 컨테이너명을 지어줬지만 이번에는 frontend-con이라는 이름을 지어준다

-   -v는 볼륨의 약자인데 컨테이너의 특정 폴더를 공유
-   코드를 짠 후 그 파일을 거실 탁자에 두면 그 거실 탁자는 Node.js가 일하는 컨테이너의 /home/node/app 서랍과 연결된 것
-   pwd는 현재 디렉터리
-   컨테이너가 언제 몇개가 만들어지든 각 컨테이너의 app 서랍에서는 거실에 둔 파일들로 얼마든지 서비스를 실행
-   이를 통하여 CMD ["http-server", "-p", "8080", "./public"]로 파일 실행이 가능한 것이다

#### Port 설명

-   -p는 포트
-   컨테이너는 CMD ["http-server", "-p", "8080", "./public"]를 통하여 8080 포트로 송출할 거니까
    집에서도 같은 곳으로 송출한다는 의미이다

---

### Dockerfile database file

-   FROM mysql:5.7 : mySql 사용하겠다

-   환경변수 : 어떤 사용자? 비번? 디비명? 등등 설정
-   ENV MYSQL_USER mysql_user
-   ENV MYSQL_PASSWORD mysql_password
-   ENV MYSQL_ROOT_PASSWORD mysql_root_password
-   ENV MYSQL_DATABASE visitlog

-   COPY ./scripts/ /docker-entrypoint-initdb.d/ : script 안의 파일들을 이미지 내부의 /docker-entrypoint-initdb.d/로 저장
-   mysql이 실행이 될 때 /docker-entrypoint-initdb.d/안의 명령어들을 실행
-   script 파일들은 컨테이너 초기화 과정에서 필요한 것들이니까 copy로 이미지 안에 미리 넣어두는 것이 좋을 것이다

#### copy와 run의 차이점

-   copy는 run처럼 이미지를 생성하는 과정에서 해당 이미지 안에 특정 파일을 미리 넣어두는 것이고
-   volume은 CMD 처럼 컨테이너가 생성되어 실행될 때 그 내부의 폴더를 외부의 것과 연결하는 것이다!!!

#### Dokcerfile 실행

-   docker build -t database-img .
-   docker run --name database-con -p 3306:3306 database-img
-   컨테이너명과 포트만 지정하면 됨 -> 실전에서는 데이터를 유지해야 하니까 데이터 폴더를 -v 옵션으로 집의 데이터 창고와 볼륨 창고를 연동할 것이다

-   docker run --name database-con -p 3306:3306 -d database-img : daemon의 줄임말, 뒤의 안보이는 곳에 가서 알아서 컨테이너 설치 및 실행...

-   현재 어떻게 실행되는지 보고 싶다면 : docker logs -f database-con

---

### Dockerfile backend file

-   FROM python:3.8.5
-   RUN pip3 install flask flask-cors flask-mysql : flask로 api를 돌림
-   WORKDIR /usr/src/app
-   CMD ["python3", "backend.py"] : 백엔드 서버를 실행

---

### docker-compose

-   이처럼 서비스를 구성하는 3개의 요소가 각각의 폴더에 Dockerfile를 통해 도커에서 어떻게 실행될지 설정이 되어 있는 것이다
-   각각의 네트워크로 분리되어 있기 때문에 백엔드와 데이터베이스는 데이터를 주고 받지 못한다

-   요소 연결 및 서비스 간편하게 실행?
-   이를 위해 사용되는 것이 거시적인 설계도인 docker-compose
-   version: '3' : 버전이며 지금의 최신 버전이 3이다
-   각각의 docker의 내용들이 services란 항목의 내부 항목들로 들어간다

#### docker-compose 내용 설명

-   항목명은 각 서비스들의 이름 (database:) 이며 이들간의 네트워크에서 각각의 호스트명이 된다
-   build: 는 도커 파일의 위치이다 compose 파일로부터..
-   ports: 는 외부에 개방할 포트이다

-   run 실행마다 작성해야되었던 명령어를 문서로 미리 작성한 것이다

-   backend에서는 volume을 사용하기 때문에 volumes:를 작성한다
-   환경 변수도 compose에서 environment:로 미리 설정할 수 있다

#### docker-compose 실행

-   docker-compose/yml이 있는 위치에서
-   docker-compose up을 실행
-   docker-compose up -d를 하면 뒤에서 알아서 컨테이너 생성 및 실행

---

## 마무리

-   이를 통하여 어느 서버에서든 도커 환경만 설치되어 있으면 git 등으로 이 프로젝트를 다운 받고 도커를 실행해서 이 컴퓨터와 똑같은 환경을 조성하고 문제없이 서비스를 돌릴 수 있을 것이다!!!
-   추가 라이브러리들을 일일히 하지 않아도 된다.
-   구름 IDE는 도커 기반의 서비스이다 -> 도커 안의 도커 설치는 현재에서는 안된다
-   윈도우에서는 WSL로 실습할 수 있지만 오류가 많을 수도 있음

-   우분투에서는 ubuntu onstall docker를 검색한 후에 도커 설치할 수 있고 docker-compose도 따로 설치해야 함
-   docker-compose up
