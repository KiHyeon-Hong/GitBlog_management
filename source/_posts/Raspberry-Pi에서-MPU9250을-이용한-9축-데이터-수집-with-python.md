---
title: Raspberry Pi에서 MPU9250을 이용한 9축 데이터 수집 with python
date: 2021-11-15 21:40:01
tags:
    - Raspberry Pi
    - MPU9250
    - I2C
    - Python
categories:
    - Raspberry Pi
    - Python
---

## 참고 사이트

-   https://medium.com/@niru5/hands-on-with-rpi-and-mpu9250-part-3-232378fa6dbc

## MPU9250 9축 센서 모듈 연결

-   MPU9250은 3축 가속도 센서, 3축 자이로 센서, 그리고 3축 지자기 센서를 통합한 센서이다.

<p align="center"><img src="/images/RaspberryPi/MPU9250/MPU9250.jpeg"></p>

-   사용하는 핀은 3.3v, GND, SDA, 그리고 SCL이며, 다음과 같이 연결한다.

<p align="center"><img src="/images/RaspberryPi/MPU9250/MPU9250_detail.png"></p>

-   연결 후 테스트

```bash
$ i2cdetect -y 1
```

## Python 모듈 설치

```bash
$ pip3 install imusensor
$ pip3 install easydict
```

## 테스트 코드

```python
import os
import sys
import time
import smbus

from imusensor.MPU9250 import MPU9250

address = 0x68
bus = smbus.SMBus(1)
imu = MPU9250.MPU9250(bus, address)
imu.begin()

while True:
	imu.readSensor()
	imu.computeOrientation()

	print ("Accel x: {0} ; Accel y : {1} ; Accel z : {2}".format(imu.AccelVals[0], imu.AccelVals[1], imu.AccelVals[2]))
	print ("Gyro x: {0} ; Gyro y : {1} ; Gyro z : {2}".format(imu.GyroVals[0], imu.GyroVals[1], imu.GyroVals[2]))
	print ("Mag x: {0} ; Mag y : {1} ; Mag z : {2}".format(imu.MagVals[0], imu.MagVals[1], imu.MagVals[2]))
	print ("roll: {0} ; pitch : {1} ; yaw : {2}".format(imu.roll, imu.pitch, imu.yaw))
	time.sleep(0.1)
```

## 추후 작업을 위한 추가 설치

-   예를 들어, Raspberry Pi의 전원이 들어오는 동시에 측정을 하고자 한다면, root 계정에 Python 모듈의 추가 설치가 필요하다.

```bash
$ su
$ sudo pip3 install imusensor
$ sudo pip3 install easydict
```
