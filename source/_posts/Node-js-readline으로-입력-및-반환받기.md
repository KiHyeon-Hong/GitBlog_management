---
title: Node.js readline으로 입력 및 반환받기
date: 2022-01-27 10:31:56
tags:
  - javascript
categories:
  - Javascript
---

## readline

- readline 모듈은 한 번에 한 줄씩 Readable 스트임에서 데이터를 읽기 위한 인터페이스를 제공한다.
- readline.createInterface()를 통해 생성 가능하며, close()를 통해 입력받는 것을 종료한다.

## 사용 예시

### 한줄 씩 입력받기

- 한줄씩 입력 받으며, 'quit', 'exit', 그리고 ctrl + c 입력 때까지 반복한다.

```javascript
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

function main() {
  rl.setPrompt(`Input data: `);
  rl.prompt();
}

rl.on('line', function (data) {
  switch (data) {
    case 'quit':
    case 'exit':
      rl.close();
  }

  console.log(`Output data: ${data}\n`);
  main();
});

rl.on('close', () => {
  console.log();
  console.log('exit...');
  process.exit();
});

main();
```

### 일정 횟수 입력받기

- 5번 입력 받으며, 입력 종료 후 입력된 정보를 출력한다.

```javascirpt
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

let question = ['첫 번째 질문', '두 번째 질문', '세 번째 질문', '네 번째 질문', '다섯 번째 질문'];
let answer = [];
let cnt = 0;

function questionFunc() {
  rl.setPrompt(`${question[cnt]}: `);
  rl.prompt();
}

rl.on('line', function (data) {
  switch (data) {
    case 'quit':
    case 'exit':
      rl.close();
  }

  answer.push(data);

  cnt++;

  if (cnt < question.length) questionFunc();
  else rl.close();
});

rl.on('close', function () {
  console.log();

  question.map((v, i) => {
    console.log(`${v}에 대한 답: ${answer[i] === undefined ? '질문에 대답하지 않음' : answer[i]}`);
  });

  process.exit();
});

questionFunc();
```

### 입력 후 비동기 처리하기

- 입력된 정보를 일정 시간(5,000ms) 후 출력한다.
- 출력 후 다시 입력을 받도록 한다.

```javascript
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

function main() {
  rl.setPrompt(`Input data: `);
  rl.prompt();
}

function asynchronous(data) {
  return new Promise((resolve) => {
    setTimeout(() => {
      return resolve(data);
    }, 5000);
  });
}

rl.on('line', async function (data) {
  switch (data) {
    case 'quit':
    case 'exit':
      rl.close();
  }

  console.log(`Output data(5,000ms...): ${await asynchronous(data)}\n`);
  main();
});

rl.on('close', () => {
  console.log();
  console.log('exit...');
  process.exit();
});

main();
```
