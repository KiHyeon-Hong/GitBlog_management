---
title: Raspberry Pi 부팅 시 IP 주소 서버로 전송하기
date: 2022-03-28 21:13:51
tags:
  - Raspberry Pi
categories:
  - Raspberry Pi
---

## 개요

- 라즈베리 파이가 부팅이 될 시, 실행 중인 서버로 IP 주소를 전송한다.
- 이를 위해, Node.js 기반의 Express.js와 Request 모듈을 이용한다.

## 서버 소스 코드

- 이를 위해, npm 모듈을 설치한다.

```bash
npm i express
npm i body-parser
```

- 소스 코드를 작성한다.

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const fs = require('fs');

const app = express();
app.use(express.json());
app.use(bodyParser.urlencoded({ extended: false }));

fs.writeFileSync('log.txt', '', 'utf8');

app.get('/', (req, res, next) => {
  let today = new Date();

  console.log(today.toLocaleString() + ': ' + req.query.ip);
  fs.appendFileSync('log.txt', today.toLocaleString() + ': ' + req.query.ip + '\n', 'utf8');
  res.send(today.toLocaleString() + ': ' + req.query.ip);
});

app.get('/get', (req, res, next) => {
  let data = fs.readFileSync('log.txt', 'utf8');
  data = data.split('\n');
  res.send(data);
});

app.listen(65001, () => {
  console.log('Server Running 65001...');
});
```

## Raspberry PI 소스 코드

- https://kihyeon-hong.github.io/2021/11/24/Raspberry-Pi-부팅-시-프로그램-자동-수행/
- rc.local 파일을 수정하여, 부팅 시 프로그램을 실행 할 때, 무선 네트워크를 잡기 전에 프로그램이 실행된다. 따라서, '127.0.0.1'이 출력이 되며, 서버로 전송이 불가능하다.
- 따라서, 무선 네트워크를 잡은 후, 전송이 되도록, 프로그램을 수정한다.

- 이를 위해, npm 모듈을 설치한다.

```bash
npm i request
npm i ip
```

- 소스 코드를 작성한다.

```javascript
const request = require('request');
const ip = require('ip');

while (ip.address() == '127.0.0.1') {}

// 192.9.200.102 -> 서버의 IP로 변경한다.
request.get({ url: `http://192.9.200.102:65001?ip=${ip.address()}` }, function (_1, _2, body) {});
```

- 이 후, 해당 소스 코드를 Raspberry PI 부팅 시, 실행되도록 설정한다.
