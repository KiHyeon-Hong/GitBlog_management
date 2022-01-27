---
title: Ubuntu 환경에서 Node.js와 Python 설치 및 관리
date: 2022-01-27 18:34:49
tags:
  - Ubuntu
  - Python
  - Node.js
categories:
  - Ubuntu
---

## Node.js 설치

- https://github.com/nodesource/distributions
- 우분투는 기본적으로 Node.js가 설치되어 있지 않다. 따라서 이를 설치하고 관리하고자 한다.

```bash
curl -fsSL https://deb.nodesource.com/setup_12.x | sudo -E bash -
sudo apt-get install -y nodejs
```

### Node.js 버전 관리

- https://github.com/nvm-sh/nvm
- nvm은 노드 버전을 쉽게 관리할 수 있게 해준다.

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```

- nvm을 zsh가 읽을 수 있게 해줘야 한다.
- 만약 설치 후 nvm 명령어가 먹히지 않는다면 다음과 같은 명령어를 ~/.zshrc에 추가한다.

```rc
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

- 설정 후 변경이 가능한 모든 Node.js의 버전을 확인한다.

```bash
nvm ls-remote
```

- 노드 버전을 설치한다.

```bash
nvm install v16.13.1
node -v
```

## Python 설치

- 파이썬은 기본적으로 python3 명령어를 통해 실행할 수 있다.
- 그러나, 버전 관리를 위해 좀 더 추가하도록 한다.

### 개인 페이지 (PPA) 추가

- https://launchpad.net/~deadsnakes/+archive/ubuntu/ppa

```bash
sudo add-apt-repository ppa:deadsnakes/ppa
엔터
sudo apt-get update
```

- 파이썬 3.8을 설치한다.

```bash
sudo apt-get install python3.8
```

- python3.8 명령어는 매우 귀찮으므로, ~/.zshrc 파일을 수정한다.

```rc
alias python=python3.8
```

- 이를 통해 python 명령어로 python3.8을 실행할 수 있다.
