---
title: Raspberry Pi 4 초기 세팅하기
date: 2021-11-15 21:16:39
tags:
    - Raspberry Pi
categories:
    - Raspberry Pi
---

## Download

-   http://www.etcher.io
-   https://www.raspberrypi.org/downloads/raspbian

## 중요 설정

```bash
$ sudo raspi-config
```

-   System Option

    -   Boot/Auto Login -> B4

-   Interface Option

    -   SSH -> enable
    -   I2C -> enable

-   Localisation Option

    -   Locale -> en_GB.UTF-8, en_US.UTF-8, ko_KR.UTF-8 -> OK
    -   Timezone -> Asia/Seoul

-   Reboot 여부를 묻는 화면에 No를 선택

## 언어 설정

```bash
$ sudo apt-get install ibus
$ sudo apt-get -y install ibus-hangul
$ sudo apt-get -y install fonts-unfonts-core

$ sudo reboot
```

## root 계정 암호 설정

```bash
$ sudo passwd root
새 UNIX 암호:
$

exit
```
