---
title: Raspberry Pi 4 gpio 시작하기
date: 2021-11-15 21:23:47
tags:
  - Raspberry Pi
  - gpio
categories:
  - Raspberry Pi
---

## Node.js 설치

```bash
$ mkdir download
$ cd download
$ wget https://nodejs.org/dist/v8.11.4/node-v8.11.4-linux-armv7l.tar.xz
$ tar -xvf node-v8.11.4-linux-armv7l.tar.xz
$ cd node-v8.11.4-linux-armv7l
$ sudo cp -R * /usr
$ cd ../..

$ node -v
V8.11.4

$ npm -v
5.6.0

$ gpio -v
gpio version: 2.46
```

## Raspberry Pi 4에서의 에러

```bash
$ gpio readall  // error
```

- Raspberry Pi 3에서는 실행되는 명령어
- Raspberry Pi 4에서는 에러가 발생
- 이는 루트 계정으로 접속하여 wiringpi를 업데이트 해준다.

```bash
$ su
$ wget https://project-downloads.drogon.net/wiringpi-latest.deb
$ sudo dpkg -i wiringpi-latest.deb
```

- 루트 계정으로 접속하지 않으면 권한때문에 다운로드가 불가능하다.

```bash
$ gpio readall
$ exit
```

## gpio 테스트

- Raspberry Pi 4에 LED를 연결 후 테스트

<p align="center"><img src="/images/RaspberryPi/gpio/gpio.jpg"></p>

```bash
$ npm install node-wiring-pi
```

```javascript
const gpio = require('node-wiring-pi');

const LEDPIN = 29;
var count = 0;

const TimeOutHandler = function () {
  if (count > 0) {
    gpio.digitalWrite(LEDPIN, 1);
    console.log('Node: LED on');
    count = 0;
  } else {
    gpio.digitalWrite(LEDPIN, 0);
    console.log('Node: LED off');
    count = 1;
  }
  setTimeout(TimeOutHandler, 1000);
};

gpio.setup('wpi');
gpio.pinMode(LEDPIN, gpio.OUTPUT);
setTimeout(TimeOutHandler, 1000);
```
