---
title: Raspberry Pi에 code-server 설치하기
date: 2022-01-27 16:45:24
tags:
  - Raspberry Pi
  - Code-server
categories:
  - Raspberry Pi
---

## Code-server란?

- 아이패드를 구입하고, 아이패드를 이용한 코딩을 하려고 시도하였지만, 아이패드에는 마땅한 어플이 존재하지 않는다.
- 따라서, 웹 브라우저를 이용해 서버의 환경에서 코딩을 할 수 있는 code-server를 이용하고자 한다.
- 이를 위해 goormide를 이용한 code-server를 구축하였지만, 이는 goormide가 켜저 있어야 하며, 이는 유료 플랜에서만 지원한다.
- 따라서, Raspberry Pi를 이용해 code-server를 구축하고, 이를 포트포워딩 하여 24시간 언제 어디에서나 코딩을 할 수 있는 환경을 구축하고자 한다.

## Code-server의 한계점

- 라즈베리파이에 보통 설치하는 운영체제는 라즈비안이다. 이는 32bit 운영체제만 지원하며, code-server가 지원하지 않아 동작이 불가능하다.
- 이를 해결하기 위해 라즈베리 파이에 64bit 운영체제인 우분투를 설치하여 해결한다.

## Raspberry Pi 우분투 설치

- https://www.balena.io/etcher/ : SD카드를 라이브 USB로 만들기 위해 압축 폴더 뿐 아니라 iso파일, .img파일과 같은 이미지 파일을 저장매채에 기록하는 데 사용하는 무료 오픈 소스 유틸리티
- https://ubuntu.com/download/raspberry-pi : 라즈베리파이 전용 우분투 (Ubuntu Desktop을 다운로드 한다.)

<p align="center"><img src="/images/RaspberryPi/code-server/RaspCodeServer1.JPG"></p>

- Flash하여 SD카드에 우분투를 설치한다.

### 주의 사항

- SD카드 파티션 재설정 후 포맷을 하지 않는다 -> 오류가 발생
- F: 드라이브의 디스크를 사용하기 전에 포맷해야 합니다. -> 취소

## 초기 설정

- Welcome -> 한국어
- 키보드 레이아웃 -> Korean -> Korean (English(US)도 상관없다)
- 무선네트워크 설정
- 거주지 -> Seoul
- 당신은 누구십니까?
  - 이름: user
  - 암호 선택: gachon654321
  - 암호 확인: gachon654321
  - 자동으로 로그인 (선택)

### Terminal 설치

```bash
sudo apt-get install -y curl
sudo apt-get install vim
sudo apt install net-tools
sudo apt install openssh-server
sudo apt install nodejs
```

## Code-server 설치

- code-server를 설치한다.

```bash
curl -fsSL https://code-server.dev/install.sh | sh
```

- 실행 후 ctrl + c를 통해 종료한다.
- 처음 실행을 하여야 설정 파일이 생성된다.
- 설정 파일에서 접속 아이피와 비밀번호를 입력한다. 초기 비밀번호는 랜덤적인 문자열이므로, 반드시 수정하여야 한다.

```bash
vim ~/.config/code-server/config.yaml
```

```text
bind-addr: 127.0.0.1:8080
auth: password
password: ~~~~
cert: false
```

```text
bind-addr: 0.0.0.0:8080
auth: password
password: gachon654321
cert: false
```

- bind-addr은 0.0.0.0:8080으로 수정한다.
- password는 원하는 비밀번호로 수정한다.

## code-server 재실행

```bash
code-server
```

- 비밀번호를 입력한 후 code-server를 이용할 수 있다.

<p align="center"><img src="/images/RaspberryPi/code-server/RaspCodeServer2.png"></p>

## 포트포워딩

- 포트포워딩을 이용하여 외부에서 접속이 가능하다.

<p align="center"><img src="/images/RaspberryPi/code-server/RaspCodeServer3.png"></p>

## nohup을 이용한 부팅 시 자동 실행 방법

- nohup는 "no hangups"라는 의미로, 쉘 스크립트 파일을 데몬 형태로 실행하는 명령이다. 터미널이 끊겨도 실행한 프로세스는 계속 동작하게 된다.
- &를 추가하여 백그라운드로 실행시킨다.

```bash
nohup code-server &
```

### 부팅 시 실행 방법

- 사용자의 메인 디렉터리에서 scripts.sh 파일에 부팅시 실행할 명령어를 입력한다.

```bash
vi scripts.sh
```

```sh
nohup code-server &
```

- :wq로 저장한다.
- sh파일의 권한을 변경하여 실행이 가능하도록 한다.

```bash
chmod +x scripts.sh
```

- crontab 명령어를 실행해서 예약 파일을 편집한다.

```bash
crontab -e
```

- 맨밑에 추가한다.

```text
@reboot /home/user/scripts.sh
```

- 리부트 한다.

```bash
reboot
```
