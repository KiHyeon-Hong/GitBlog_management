---
title: Docker에서 Host IP 이용하기
date: 2022-04-07 21:26:52
tags:
  - docker
categories:
  - docker
---

## Docker에서 Host IP 이용하기

- Docker에서 IP를 확인하면, Host IP가 아닌 Docker 컨테이너의 IP가 확인된다.
- 이를 해결하기 위해, Docker를 run 하는 과정에서 Docker의 IP를 Docker가 동작하고 있는 호스트의 IP로 매핑한다.

```bash
docker run -p <호스트포트>:<컨테이너포트> -d <이미지명>
```

- 위와 같이 run을 사용하면, Docker의 IP는 매핑이 되지 않는다.

```bash
docker run -p <호스트포트>:<컨테이너포트> -d --network="host" <이미지명>
```

- Docker의 IP를 호스트의 IP로 매핑하기 위해 --network 플래그를 사용한다.

## 사용 예시

- 이를 테스트하기 위해, 간단한 코드를 작성한다.
- 해당 소스 코드는 Docker가 동작하고 있는 환경의 공인 IP와 사설 IP를 반환하는 웹 페이지를 작성한다.

### npm 모듈 환경 설정

```bash
npm i express
npm i ip
npm i public-ip
```

### 소스 코드

#### ./index.js

```javascript
const express = require('express');
const app = express();

app.get('/', async (req, res, next) => {
  const ip = require('ip');
  const publicIp = await import('public-ip');

  res.send(`공인 IP: ${await publicIp.default.v4()}, 사설 IP: ${ip.address()}`);
});

app.listen(65011, () => {
  console.log(`Server running...`);
});
```

#### ./Dockerfile

```text
FROM node:16

WORKDIR /usr/src

COPY package*.json ./
RUN npm install
COPY . .

EXPOSE 65011

CMD [ "node", "index.js" ]
```

#### ./.dockerignore

```text
node_modules
npm-debug.log
```

### 소스 코드 실행

- Docker 이미지를 생성한다.

```bash
docker build . -t testimage
```

<p align="center"><img src="/images/Docker/HostIP/dockerHostIp1.jpg"></p>

## 실행 비교

### --network 플래그 미사용

```bash
docker run -p 65006:65006 -d testimage
```

- 플래그를 사용하지 않으면, 172.xx로 시작하는 Docker의 IP가 뜨는 것을 볼 수 있다.

<p align="center"><img src="/images/Docker/HostIP/dockerHostIp2.jpg"></p>

<p align="center"><img src="/images/Docker/HostIP/dockerHostIp3.jpg"></p>

### --network 플래그 사용

```bash
docker run -p 65006:65006 -d --network="host" testimage
```

- 플래그를 사용한다면, 192.xx로 시작하는 호스트의 IP가 뜨는 것을 볼 수 있다.

<p align="center"><img src="/images/Docker/HostIP/dockerHostIp4.jpg"></p>

<p align="center"><img src="/images/Docker/HostIP/dockerHostIp5.jpg"></p>
