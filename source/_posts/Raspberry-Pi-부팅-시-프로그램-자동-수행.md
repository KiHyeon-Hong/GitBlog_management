---
title: Raspberry Pi 부팅 시 프로그램 자동 수행
date: 2021-11-24 20:25:39
tags:
  - Node.js
  - Raspberry Pi
  - Telegram
categories:
  - Raspberry Pi
---

#### 텔레그램 서버를 라즈베리 파이가 부팅하는 동시에 실행하여 별도의 디스플레이 없이 ssh 접속 IP를 얻도록 한다.

- 라즈베리 파이가 부팅할 때 프로그램을 자동으로 수행 시키기 위해서는 루트 권한이 필요하다.
- su 명령어를 이용해 루트 계정으로 접속한다.

<p align="center"><img src="/images/RaspberryPi/BootProgram/Init/BootProgram/BootProgram1.png"></p>

- 부팅 프로그램은 /etc 디렉터리에 존재하므로 cd 명령어를 이용해 이동한다.

### 부팅 프로그램 작성 전 중요 테스트

- 부팅 프로그램에서 실수를 한다면 부팅이 되지 않는 심각한 오류에 걸릴수도 있다.
- 이를 방지하기 위해 해당 디렉터리에서 절대 경로로 작성한 코드를 테스트 한다.

```bash
node /home/user/Telegram/telegram.js
```

<p align="center"><img src="/images/RaspberryPi/BootProgram/Init/BootProgram/BootProgram2.png"></p>

- rc.local 파일을 열고 exit 0 위에 실행할 명령어를 입력한다.
- 이 때, 중요한 점은 텔레그램 봇 서버와 같이 종료가 되지 않는 프로그램의 경우 &를 붙여야 한다.
- 이를 통하여 텔레그램 봇 서버는 부팅과 별도로 수행된다.

```bash
vi rc.local


~
~
node /home/user/Telegram/telegram.js &
exit 0


:wq
```

- 라즈베리 파이를 재부팅하여 텔레그램 봇 서버가 정상적으로 동작하는 지 확인한다.

```bash
sudo reboot
```

### 획인

<p align="center"><img src="/images/RaspberryPi/BootProgram/Init/BootProgram/BootProgram3.jpg"></p>
