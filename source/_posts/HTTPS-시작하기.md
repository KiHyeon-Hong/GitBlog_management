---
title: HTTPS 시작하기
date: 2021-11-27 11:37:42
tags:
  - HTTPS
  - Node.js
categories:
  - HTTPS
---

- HTTPS(HTTP Secure)는 HTTP 프로토콜의 암호화된 버전이다.
- 클라이언트와 서버 간의 모든 커뮤니케이션을 암호화하기 위해 SSL이나 TLS를 이용한다.
- 본 포스팅에서는 HTTPS 통신을 위해 SSL을 이용한다.

## OpenSSL 설치

- http://slproweb.com/products/Win32OpenSSL.html
- 개발 및 테스트를 위해 OpenSSL을 다운로드하고 설치한다.
- 자신의 환경에 맞는 설치 파일을 다운로드하고 설치한다.
- Win64 OpenSSL v1.1.1L

<p align="center"><img src="/images/HTTPS/Init/HTTPSInit1.png"></p>

## OpenSSL 환경 변수 설정

- Path에 OpenSSL의 bin 폴더를 추가한다.

<p align="center"><img src="/images/HTTPS/Init/HTTPSInit2.png"></p>

- 터미널에 openssl을 입력하여 다음과 같은 화면이 뜨면 설정 완료

```bash
openssl
```

<p align="center"><img src="/images/HTTPS/Init/HTTPSInit3.png"></p>

## 개인키와 공유키 생성

- SSL 통신을 위해 개인키와 쌍을 이루는 공유키를 생성한다.

```bash
openssl genrsa 1024 > private.pem
openssl req -x509 -new -key private.pem > public.pem
```

## HTTPS 프로토콜 사용 예시

- Node.js를 이용한 HTTP 서버에서 HTTPS 서버로 변경한 예시
- 포트는 8080에서 3000으로 변경하였다.
- 개인키와 공유키를 받아온다.

```javascript
var http = require('http');
var socketIO = require('socket.io');

var fileServer = new nodeStatic.Server();
var app = http
  .createServer(function (req, res) {
    fileServer.serve(req, res);
  })
  .listen(8080);
```

```javascript
// var http = require('http');
const https = require('https');
var socketIO = require('socket.io');
const fs = require('fs');

const options = { key: fs.readFileSync('./private.pem'), cert: fs.readFileSync('./public.pem') };

var fileServer = new nodeStatic.Server();
let app = https
  .createServer(options, (req, res) => {
    fileServer.serve(req, res);
  })
  .listen(3000);
```

## HTTPS 서버 접속 예시

- 다음과 같이 https://localhost:3000을 이용하여 접속하는 것을 볼 수 있다.

<p align="center"><img src="/images/HTTPS/Init/HTTPSInit4.png"></p>
