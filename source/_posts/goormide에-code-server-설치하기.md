---
title: goormide에 code-server 설치하기
date: 2022-01-27 11:33:25
tags:
  - Code-server
categories:
  - Development
  - Code-server
---

## 개발환경 설정 취지

- 아이패드를 구입하고 아이패드를 이용해 코딩을 하려고 했지만, 마땅한 어플이 존재하지 않는다.
- 따라서, 웹 브라우저로 간단하게 접속할 수 있는 code-server를 구축하여 아이패드를 이용해 코딩할 수 있는 환경을 구축하고자 한다.

## Code-server란?

- Visual studio code를 Node.js를 통해 Server에 올리고, 이를 웹 브라우저를 이용해 접속하는 프로그램이다.
- 이를 위해 접속할 환경에 code-server가 설치되어 있어야 하며, 이는 실행되어 있어야 한다.
- 외부에서 접속하기 위해 포트포워딩을 하여야 한다.

## https://vscode.dev/와의 차이점

- https://vscode.dev/는 웹 브라우저를 이용해 로컬 환경에서 코딩을 하는 사이트이다. 이는 로컬 환경의 파일을 열어볼 수 없는, 또는 열기 힘든 아이패드와 같은 환경에서 적절하지 못하다.
- 그에 비해 code-server는 외부의 파일 디렉터리에 원격으로 접속하여 프로그래밍을 하므로, 아이패드의 제한적인 환경에 구애받지 않는다.

## goormide 설명

- goormide는 웹 기반 클라우드 코딩 서비스이다.
- 컨테이너 기반의 개발 환경을 구축해준다.

## goormide를 이용한 code-server 설치

- goormide의 컨테이너를 생성하며, 공개 범위는 public, 소프트웨어 스택은 node.js를 선택한다.
- 다음과 같은 명령어를 입력하여 code-server를 설치한다.

```bash
vim ~/.config/code-server/config.yaml
```

- code-server를 실행하여 설정 파일을 생성한다.

```bash
root@goorm:/workspace/code-server# code-server
[2022-01-27T02:49:15.646Z] info  Wrote default config file to ~/.config/code-server/config.yaml
[2022-01-27T02:49:18.522Z] info  code-server 4.0.1 735c6da829535969ff7193c79379299e4a1cb9bc
[2022-01-27T02:49:18.525Z] info  Using user-data-dir ~/.local/share/code-server
[2022-01-27T02:49:18.555Z] info  Using config file ~/.config/code-server/config.yaml
[2022-01-27T02:49:18.555Z] info  HTTP server listening on http://127.0.0.1:8080/
[2022-01-27T02:49:18.556Z] info    - Authentication is enabled
[2022-01-27T02:49:18.619Z] info      - Using password from ~/.config/code-server/config.yaml
[2022-01-27T02:49:18.619Z] info    - Not serving HTTPS
```

- ctrl+c로 종료 후 설정 파일을 연다.

```
vi ~/.config/code-server/config.yaml
```

<p align="center"><img src="/images/Development/Code-server/Goormide/goormide1.png"></p>

- 주소를 0.0.0.0:8080으로 수정한다.
- 비밀번호를 원하는 비밀번호로 수정한다.
- :wq 명령을 이용해 저장한다.

<p align="center"><img src="/images/Development/Code-server/Goormide/goormide1.png"></p>

- code-server를 재실행한다.

```bash
code-server
```

## 포트포워딩

- goormide는 포트포워딩을 제공한다.
- 오른쪽 상단의 미리보기에서 실행 URL과 포트 설정을 선택한다.

<p align="center"><img src="/images/Development/Code-server/Goormide/goormide3.png"></p>

- URL과 포트를 설정한다. 이때, 포트는 설정 파일에서 저장한 포트인 8080으로 한다.

<p align="center"><img src="/images/Development/Code-server/Goormide/goormide4.png"></p>

- 웹브라우저를 이용해 해당 URL에 접속하면, 다음과 같은 화면이 나온다.
- 비밀번호를 입력한다.

<p align="center"><img src="/images/Development/Code-server/Goormide/goormide5.png"></p>

- goormide의 디렉터리가 화면에 출력되는 것을 볼 수 있다.
