---
title: PyScript를 이용하여 HTML에서 python 실행하기
date: 2022-05-29 00:28:09
tags:
  - Python
categories:
  - Python
---

## 참고 자료

- https://www.youtube.com/watch?v=3DuyJf_XPtM

## PyScript

- PyScript는 프레임워크로 HTML에서 python을 이용하여 다이나믹 어플리케이션을 빌드할 수 있게 하는 도구이다.

## 이벤트를 이용한 기본 예제 코드

- index.html에서 숫자를 선택하고 버튼을 클릭하면, 이벤트가 발생하여 main.py의 메소드가 실행된다.
- main.py에서는 동작을 수행하고, 결과는 index.html 태그에 결과 메시지를 저장한다.

### index.html

```html
<!DOCTYPE html>
  <head>
    <script defer src="https://pyscript.net/alpha/pyscript.js"></script>
    <link rel="stypesheet" href="'https://unpkg.com/@picocss/pico@latest/css/pico.min.css" />
  </head>
  <body>
    <py-script src="./main.py"></py-script>
    <main class="container">
      <div>
        <input type="number" id="number_input" min="1" max="50" placeholder="Guess a number 1 and 50" />
        <button id="add_todo" pys-onClick="play_game" >Guess</button>
      </div>
      <h1 id="result"></h1>
    </main>
  </body>
</html>
```

### main.py

```python
import random

number_input = Element("number_input")
result = Element("result")

def play_game(*args):
  user_guess = number_input.value
  machine_guess = random.randint(1, 50)


  if int(user_guess) == machine_guess:
    result.element.innerText = "You Win!"
  else:
    result.element.innerText = f"You Lost! The machine chose {machine_guess}!"
  number_input.clear()
```

### 실행 결과

- 처음 실행 화면은 다음과 같다.

<p align="center"><img src="/images/Python/PyScript/PyScript_start/PyScript_test_code1.jpeg"></p>

- 1 ~ 50까지 선택한 숫자와 컴퓨터가 선택한 숫자가 일치하지 않는 경우 다음과 같은 메시지가 출력된다.

<p align="center"><img src="/images/Python/PyScript/PyScript_start/PyScript_test_code2.jpeg"></p>

- 1 ~ 50까지 선택한 숫자와 컴퓨터가 선택한 숫자가 일치할 경우 다음과 같은 메시지가 출력된다.

<p align="center"><img src="/images/Python/PyScript/PyScript_start/PyScript_test_code3.jpeg"></p>

## Python의 외부 모듈 이용하기

- numpy와 같은 외부 모듈을 import하여 사용할 수 있다.

```html
<html>
  <head>
    <title>Matplotlib</title>
    <meta charset="utf-8" />

    <link rel="stylesheet" href="https://pyscript.net/alpha/pyscript.css" />
    <script defer src="https://pyscript.net/alpha/pyscript.js"></script>
    <py-env> - matplotlib </py-env>
  </head>
  <body>
    <div id="mpl"></div>
    <py-script output="mpl"> import matplotlib.pyplot as plt plt.plot([1, 2, 3, 4], [10, 20, 40, 30]) plt </py-script>
  </body>
</html>
```

### 실행 결과

- 실행 결과는 다음과 같다.

<p align="center"><img src="/images/Python/PyScript/PyScript_start/PyScript_test_code4.jpeg"></p>
