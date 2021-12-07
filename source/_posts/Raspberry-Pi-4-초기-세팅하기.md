---
title: Raspberry Pi 4 초기 세팅하기
date: 2021-11-15 21:16:39
tags:
  - Raspberry Pi
categories:
  - Raspberry Pi
---

## Download

- http://www.etcher.io
- https://www.raspberrypi.org/downloads/raspbian

## 중요 설정

```bash
$ sudo raspi-config
```

```text
1. System Options
	S5. Boot / Auto Login Select boot into desktop or to command line
		B4. Desktop Autologin Desktop GUI, automatically logged in as 'pi' user


3. Interface Options
	P2. SSH -> Yes
	P5. I2C -> Yes


5. Localisation Options
	L1. Locale
		en_GB.UTF-8 UTF-8
		en_US.UTF-8 UTF-8
		ko_KR.UTF-8 UTF-8

		ko_KR.UTF-8 UTF-8 -> Ok

	L2. TimeZone
		Asia/Seoul


Finish -> Reboot? -> No
```

## 언어 설정

```bash
$ sudo apt-get install ibus
$ sudo apt-get -y install ibus-hangul
$ sudo apt-get -y install fonts-unfonts-core

$ sudo reboot
```

## root 계정 암호 설정

- su 명령어를 사용하기 위해 필수적으로 설정

```bash
$ sudo passwd root
새 UNIX 암호:
$

exit
```
