---
title: Raspbian Docker 설치하기
date: 2022-01-27 13:20:38
tags:
  - Raspberry Pi
  - docker
categories:
  - Raspberry Pi
  - docker
---

## Docker 설치하기

- Raspbian은 Docker가 기본으로 설치되어 있지 않으므로, apt를 이용해 설치하는 과정이 필요하다.

```bash
apt install docker.io
docker -v
```

## Docker 예제 실행하기

- 설치된 Docker를 이용해 예제를 빌드하고 실행한다.
- 해당 예제는 express.js 위에서 REST API 형태로 제공되는 기능이므로, Docker 내부의 포트를 외부의 포트와 연결하여야 한다.

```bash
docker build . -t passwordsecurityserver
docker run -p 65001:65001 -d passwordsecurityserver
```

- 해당 컨테이너의 bash로 들어가기 위해서는 다음과 같이 exec 명령어를 사용한다.

```bash
docker exec -it <container ID> /bin/bash
```

## 예제 실행하기

- run 명령어를 통해 docker는 실행중이며, 다음과 같이 확인할 수 있다.

```
# GET
http://localhost:65001/passwordModelTrain?versionData=0.2&comment=TestComment
```

- localhost:65001 : 비밀번호 보안성 학습모듈이 실행중인 IP와 포트
- versionData=0.2 : 학습을 요청할 모델 버전
- comment=TestComment : 코멘트

```json
// 버전 중복
{
    "state": 301,
    "comment": "0.1은 중복된 버전"
}

// 학습 정상 동작
{
  "state": 200,
  "comment": "0.2 model 학습 시작"
}
```
