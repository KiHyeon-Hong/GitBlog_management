---
title: Googletrans 모듈을 이용한 번역 사이트
date: 2022-05-29 00:12:00
tags:
  - Python
categories:
  - Python
---

## Googletrans 설치하기

- pip install googletrans는 오류가 발생하므로, 기존 버전을 설치하여야 한다.

```bash
pip install googletrans==4.0.0-rc1
```

## googletrans 테스트

- 한글을 영어로 바꾸는 예시와 영어를 한글로 바꾸는 예시를 테스트한다.

```python
import googletrans
translator = googletrans.Translator()

print(translator.translate("이것은 테스트 메시지 입니다.", src='ko', dest='en').text)
print(translator.translate("This is a test message.", src='en', dest='ko').text)
```

```bash
This is a test message.
이것은 테스트 메시지입니다.
```

## flask 설치하기

```bash
pip install flask
```

## 간단한 번역 웹 페이지 소스 코드

```python
from flask import Flask, request
import googletrans

app = Flask(__name__)
translator = googletrans.Translator()

@app.route('/ko2en')
def ko2en():
    str = request.args.get('str')
    return translator.translate(str, src='ko', dest='en').text

@app.route('/en2ko')
def en2ko():
    str = request.args.get('str')
    return translator.translate(str, src='en', dest='ko').text

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=65001)
```

## 테스트

- 웹 페이지를 실행 후, 다음과 같이 접속을 테스트한다.
- http://localhost:65001/ko2en?str=사람입니다

```text
I am a person
```
