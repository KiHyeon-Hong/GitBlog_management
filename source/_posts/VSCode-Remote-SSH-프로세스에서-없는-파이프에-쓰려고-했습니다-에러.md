---
title: VSCode Remote-SSH 프로세스에서 없는 파이프에 쓰려고 했습니다 에러
date: 2021-12-07 20:45:10
tags:
  - VSCode
  - Error
  - Remote-SSH
categories:
  - VSCode
  - Error
---

## Rempte-SSH

- Remote-SSh는 VSCode의 확장 기능 중 하나로 SSH 접속을 위한 도구

<p align="center"><img src="/images/VSCode/Remote-SSH/ProcessError/Remote-SSH.png"></p>

- Ctrl + Shift + p를 이용해 접속 가능

<p align="center"><img src="/images/VSCode/Remote-SSH/ProcessError/Error1.png"></p>

## 프로세스에서 없는 파이프에 쓰려고 했습니다 에러

- 동일한 IP를 이용해 전에 접속을 하였지만, 다른 기기나 환경이라면 다음과 같은 에러 발생

<p align="center"><img src="/images/VSCode/Remote-SSH/ProcessError/Error2.png"></p>

```bash

[20:37:25.006] Log Level: 2
[20:37:25.012] remote-ssh@0.66.1
[20:37:25.012] win32 x64

...

> 프로세스에서 없는 파이프에 쓰려고 했습니다.
[20:37:27.428] "install" terminal command done
[20:37:27.430] Install terminal quit with output: 프로세스에서 없는 파이프에 쓰려고 했습니다.
[20:37:27.431] Received install output: 프로세스에서 없는 파이프에 쓰려고 했습니다.
[20:37:27.436] Failed to parse remote port from server output
[20:37:27.440] Resolver error: Error:

...

```

## 해결 방법

- {user}/.ssh/known_hosts
- 해당 파일을 열면 다음과 같은 내용을 볼 수 있음

```text
192.168.1.106 ~
192.168.1.105 ~
192.168.0.22 ~
```

- 방금 접속을 시도한 IP 주소를 지우고 다음과 같이 저장을 수행

```text
192.168.1.106 ~
192.168.1.105 ~
```

- Remote-SSH를 이용해 재접속 실시
