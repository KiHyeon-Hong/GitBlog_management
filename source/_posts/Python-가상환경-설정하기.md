---
title: Python 가상환경 설정하기
date: 2022-01-27 11:01:26
tags:
  - Python
categories:
  - Python
---

## 파이썬 가상환경

- 파이썬의 venv 모듈은 자체 사이트 디렉터리를 갖는 경량 가상 환경을 만들고, 선택적으로 시스템 사이트 디렉터리에서 격리할 수 있도록 지원한다.
- 명령프롬프트에서 다음을 입력한다.

```bash
# 기본 명령어
python -m venv venv

# 현재의 파이썬 전역 패키지들을 깐다
python -m venv 가상환경이름 --system-site-packages
```

## 가상환경 접속

```bash
venv\Scripts\activate.bat
```

```bash
(venv) C:\Users\user>
```

- 가상환경이 활성화되었다.

## 주피터 노트북을 사용하기 위한 환경설정

- 주피터 노트북을 이용하기 위해 jupyter 모듈을 설치한다.
- 추가적으로 사용할 다양한 라이브러리를 설치한다.

```bash
pip3 install jupyter

pip3 install matplotlib
...
```

### 주피터 노트북 실행 명령어

```bash
python -m notebook
```

## 추후 접속하기

- 가상환경에 설치된 주피터 노트북을 실행하기 위해서는 다음 두 명령어를 입력한다.

```bash
venv\Scripts\activate.bat
python -m notebook
```

## 가상환경 삭제

- 가상환경의 삭제는 설치된 'venv' (가상환경 디렉터리 이름) 디렉터리 자체를 그냥 삭제해주면 된다.
