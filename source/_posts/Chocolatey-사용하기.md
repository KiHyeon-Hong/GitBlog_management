---
title: Chocolatey 사용하기
date: 2022-01-27 17:23:39
tags:
  - Windows
categories:
  - Windows
---

## Chocolatey

- Chocolatey는 Windows 소프트웨어용 명령줄 패키지 관리자 및 설치 프로그램이다.
- Windows powerSHell을 이용하여 소프트웨어를 다운로드 및 설치 프로세스를 단순화한다.
- https://chocolatey.org/
- 설치 후 바로 콘솔에서 테스트가 가능하다.
- 만약에 choco를 사용하지 않는다면 path 설정과 같은 복잡한 과정이 필요하다.
- 다음과 같은 명령어로 설치한다.

```bash
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

- 설치를 확인한다.

<p align="center"><img src="/images/Windows/Chocolatey/choco.png"></p>

### 주의 사항

- powershell을 관리자 버전으로 실행하여야 한다.

## windows terminal 설치

- choco를 이용하여 Windows Terminal을 설치한다.

```bash
choco install microsoft-windows-terminal
```

- a를 선택하여 모두 설치한다.

### 주의 사항

- powershell을 관리자 버전으로 실행하여야 한다.
