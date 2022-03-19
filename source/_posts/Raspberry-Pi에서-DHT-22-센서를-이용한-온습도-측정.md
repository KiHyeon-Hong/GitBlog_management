---
title: Raspberry Pi에서 DHT-22 센서를 이용한 온습도 측정
date: 2022-03-19 10:38:40
tags:
  - Raspberry Pi
categories:
  - Raspberry Pi
---

## DHT-22

- DHT-22 센서를 이용해 Raspberry Pi 4 model B에서 온도와 습도 데이터를 측정한다.

## Raspberry Pi 4 model B에서 gpio 핀 이용하기

- Raspberry Pi 4 model B에서 gpio핀을 이용한 센서 데이터를 받아오려고 하면, 에러가 발생한다.

```bash
$ gpio readall  // error
```

- 이를 해결하기 위해 다음과 같이 입력한다.

```bash
$ su
$ wget https://project-downloads.drogon.net/wiringpi-latest.deb
$ sudo dpkg -i wiringpi-latest.deb
```

## node-dht-sensor 에러

- BCM2835 관련 라이브러리를 설치한다.

```bash
$ curl -O http://www.airspayce.com/mikem/bcm2835/bcm2835-1.36.tar.gz
$ tar zxvf bcm2835-1.36.tar.gz
$ d bcm2835-1.36
$ ./configure
$ make
$ sudo make check
$ sudo make install
```

## node-dht-sensor 설치하기

```bash
$ npm init
$ npm install node-dht-sensor
```

## DHT-22 센서 모듈 사용 예제

```javascript
const sensorLib = require('node-dht-sensor');

const sensor = {
  sensors: [
    {
      name: 'Outdoor',
      type: 22,
      pin: 21,
    },
  ],
  read: function () {
    for (var index in this.sensors) {
      var s = sensorLib.read(this.sensors[index].type, this.sensors[index].pin);
      console.log('온도: ' + s.temperature.toFixed(1) + '°C, 습도: ' + s.humidity.toFixed(1) + '%');
    }
    setTimeout(function () {
      sensor.read();
    }, 5000);
  },
};

sensor.read();
```

```bash
node test.js
```
