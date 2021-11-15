---
title: Raspberry Pi에서 MPU9250을 이용한 9축 데이터 수집 with Node.js
date: 2021-11-15 21:49:03
tags:
    - Raspberry Pi
    - MPU9250
    - I2C
    - Node.js
categories:
    - Raspberry Pi
    - Node.js
---

## 참고 사이트

-   https://www.npmjs.com/package/mpu9250

## MPU9250 9축 센서 모듈 연결

-   MPU9250은 3축 가속도 센서, 3축 자이로 센서, 그리고 3축 지자기 센서를 통합한 센서이다.

<p align="center"><img src="/images/RaspberryPi/MPU9250/MPU9250.jpg"></p>

-   사용하는 핀은 3.3v, GND, SDA, 그리고 SCL이며, 다음과 같이 연결한다.

<p align="center"><img src="/images/RaspberryPi/MPU9250/MPU9250_detail.jpg"></p>

-   연결 후 테스트

```bash
$ i2cdetect -y 1
```

## Node.js 모듈 설치

-   모듈 설치는 권한 때문에 루트 계정으로 수행한다.

```bash
$ su
$ npm install mpu9250
```

## 테스트 코드

```javascript
var mpu9250 = require('mpu9250');

var mpu = new mpu9250({
    device: '/dev/i2c-1',
    address: 0x68,
    UpMagneto: true,
    scaleValues: true, // 전처리
    DEBUG: false,
    ak_address: 0x0c,
    GYRO_FS: 0,
    ACCEL_FS: 2,
    DLPF_CFG: mpu9250.MPU9250.DLPF_CFG_3600HZ,
    A_DLPF_CFG: mpu9250.MPU9250.A_DLPF_CFG_460HZ,
    SAMPLE_RATE: 8000,
});

mpu.initialize();

setInterval(() => {
    console.log(mpu.getMotion9());
}, 50);
```
