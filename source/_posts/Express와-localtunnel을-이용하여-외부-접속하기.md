---
title: Express와 localtunnel을 이용하여 외부 접속하기
date: 2022-02-12 12:29:50
tags:
  - Node.js
categories:
  - Node.js
---

## Express와 localtunnel을 이용하여 외부 접속하기

- Node.js의 express.js로 구축한 서버는 사설 IP로 접속 가능하며, 외부로 공개하기 위해서는 포트포워딩과 같은 추가적인 설정이 필요하다.

### localtunnel

- https://www.npmjs.com/package/localtunnel
- localtunnel은 로컬 환경에서 동작중인 서버의 포트를 외부로 공개하기 쉽도록 한 npm 모듈이다.

### forever

- https://www.npmjs.com/package/forever
- forever는 주어진 스크립트가 백그라운드에서 실행되도록 하는 간단한 cli 도구이다.
-

## 설치하기

- localtunnel과 forever를 -g로 설치한다.
- 이때, 권한 거부를 방지하기 위해 sudo 명령어로 실행한다.

```bash
sudo npm install -g localtunnel
sudo npm install -g forever
```

### 예제 소스 코드 받기

- express 실행과 동시에 localtunnel로부터 실시간으로 외부로 공개하는 url를 제공받는 예제 코드이다.
- https://github.com/KiHyeon-Hong/Localtunnel_and_forever_test_code

```bash
git clone https://github.com/KiHyeon-Hong/Localtunnel_and_forever_test_code.git
cd Localtunnel_and_forever_test_code
npm i
```

- sudo 명령어를 통해 서버를 실행하며, 실행 후 localtunnel로부터 받은 url을 파일로 저장하여 확인하는 명령어를 실행한다.

```bash
sudo forever start mainController.js && lt --port 65001 > ./files/url.txt
```

## 실행 결과

<p align="center"><img src="/images/Node_js\\/localtunnel/localtunnel1.jpg"></p>

```bash
sudo forever start mainController.js && lt --port 65001 > ./files/url.txt
```

- 위 명령어를 통해 실행한 화면이다.

<p align="center"><img src="/images/Node_js\\/localtunnel/localtunnel2.jpg"></p>

- 기본적으로 이미 알고 있는 사설 IP를 이용해 접속하면, 다음과 같이 외부로 공개하기 위한 url을 확인할 수 있다.

<p align="center"><img src="/images/Node_js\\/localtunnel/localtunnel3.jpg"></p>

- 해당 url을 복사하여 접속하면, 최초 1회 허용 메시지가 출력된다.
- Click to Cintinue를 클릭한다.

<p align="center"><img src="/images/Node_js\\/localtunnel/localtunnel4.jpg"></p>

- 제공된 url을 통해 접속이 된 것을 확인할 수 있으며, 이는 외부에서도 접속할 수 있다.

<p align="center"><img src="/images/Node_js\\/localtunnel/localtunnel5.jpg"></p>

- files/url.txt는 localtunnel로 제공받은 url이 기록된다.

## 주의사항

- 해당 예제 소스코드는 윈도우 환경에서 동작하지 않는다.
- 추가적으로 서버 종료 후 다시 실행 시 새로운 url이 발급되며, 전에 사용한 url은 동작하지 않는다.
