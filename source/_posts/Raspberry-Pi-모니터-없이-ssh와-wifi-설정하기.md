---
title: Raspberry Pi 모니터 없이 ssh와 wifi 설정하기
date: 2022-01-27 13:33:17
tags:
  - Raspberry Pi
categories:
  - Raspberry Pi
---

## Raspberry Pi의 한계점

- 라즈베리 파이를 처음 설치한 후 ssh 접속을 위해서는 무선 연결, 또는 유선 연결을 하여야 한다.
- 또한, 무선 연결이나 유선 연결을 한 후 IP주소를 알아야 한다.
- 이는 만약에 모니터가 없거나 Serial 케이블이 없다면 알 수 있는 방법이 없다.
- 이를 해결하기 위해 라즈베리 파이의 파일 설정하는 방법을 알아야 한다.

## ssh 활성화

1. 초기설정을 아직 진행하지 않은 Raspbian이 설치된 SD카드를 데스크탑에 연결한다.
2. 포맷은 진행하지 않으며, 데스크탑에 연결할 경우 boot 파티션이 나타난다.
3. boot 디렉터리에서 확장자 없이 ssh 파일을 생성한다.

## wifi 설정

1. 초기설정을 아직 진행하지 않은 Raspbian이 설치된 SD카드를 데스크탑에 연결한다.
2. 포맷은 진행하지 않으며, 데스크탑에 연결할 경우 boot 파티션이 나타난다.
3. boot 디렉터리에서 확장자 없이 wpa_supplicant.conf 파일을 생성한다.

- 라즈비안 최신 버전인 'Stretch'의 경우

```conf
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
network={
    ssid="접속하고자 하는 wifi 이름"
    psk="접속하고자 하는 wifi 비밀번호"
    key_mgmt=WPA-PSK
}
```

- 그 이전 버전

```
network={
    ssid="접속하고자 하는 wifi 이름"
    psk="접속하고자 하는 wifi 비밀번호"
    key_mgmt=WPA-PSK
}
```

- 다음과 같은 결과가 나타난다.

<p align="center"><img src="/images/RaspberryPi/sshAndWifi/bootFiles.jpg"></p>

## ssh 접속 후 wifi 설정

```bash
sudo vi /etc/wpa_supplicant/wpa_supplicant.conf
```

- priority가 높은 것을 먼저 시도한다.

```conf
network={
	ssid="~"
	psk="~"
	priority=1
	key_mgmt=WPA-PSK
}

network={
	ssid="~"
	psk="~"
	priority=2
	key_mgmt=WPA-PSK
}
```
