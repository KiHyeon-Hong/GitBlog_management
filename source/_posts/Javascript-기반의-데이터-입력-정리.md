---
title: Javascript 기반의 데이터 입력 정리
date: 2022-10-08 16:58:29
tags:
  - javascript
categories:
  - javascript
---

- Javascript 기반 코딩테스트에서 입력을 위한 readline 사용법을 정리한다.

## 1줄 입력받기

- Node.js의 readline은 비동기적으로 동작하므로, async, await를 이용한다.

```javascript
const readline = require('readline');

(async () => {
  let rl = readline.createInterface({ input: process.stdin });

  for await (const line of rl) {
    let data = line;
    console.log(data);

    rl.close();
  }

  process.exit();
})();
```

## 여러 줄 입력 받기 (readline 1개 사용)

- 코딩테스트를 하다보면 입력한 정보를 기반으로 다른 정보를 입력받아야 하는 경우가 있다.
- 이를 위해, 중첩 for문을 사용하며 조건을 통해 입력을 제한한다.

```javascript
const readline = require('readline');

(async () => {
  let rl = readline.createInterface({ input: process.stdin });

  for await (const line of rl) {
    let count = parseInt(line);

    let data = [];

    let cnt = 0;
    for await (const line of rl) {
      data.push(line);
      cnt++;

      if (count === cnt) rl.close();
    }

    console.log(data);
  }

  process.exit();
})();
```

## 여러 줄 입력 받기 (readline 여러개 사용)

- rl.close()를 통해 readline을 종료하였으므로, 새로운 rl을 선언하고 사용한다.

```javascript
const readline = require('readline');

(async () => {
  let rl = readline.createInterface({ input: process.stdin });

  let count = 0;
  for await (const line of rl) {
    count = parseInt(line);
    rl.close();
  }

  rl = readline.createInterface({ input: process.stdin });

  let data = [];

  let cnt = 0;
  for await (const line of rl) {
    data.push(line);
    cnt++;

    if (count === cnt) rl.close();
  }

  console.log(data);

  process.exit();
})();
```
