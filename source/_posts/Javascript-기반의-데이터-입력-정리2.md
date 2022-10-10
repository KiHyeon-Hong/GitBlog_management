---
title: Javascript 기반의 데이터 입력 정리2
date: 2022-10-10 21:54:18
tags:
  - javascript
categories:
  - javascript
---

- 코딩테스트 문제에서 Javascript 기반 입력을 위한 방법 정리
- 프로그래머스는 입력과 출력 예시가 함수의 파라매터 형태로 제공되므로, 입력을 신경쓰지 않는다.
- 그러나, 백준이나 구름에서는 입력과 출력을 고려하여 작성해야 한다.

## 해결 문제

- 첫 줄에는 사용자로부터 입력받을 횟수를 받는다.
- 두번째 줄부터 띄어쓰기로 구분된 2개의 숫자를 입력받으며, 입력과 동시에 출력한다.
- 입력이 모두 종료되면, 프로그램을 종료한다.

```text
3
1 2
2 4
4 6
```

```text
3
1 2
1 2
2 4
2 4
4 6
4 6
```

### Async, Await를 사용하지 않은 방법

```javascript
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

let count = 0;
let cnt = 0;
let check = 0;

rl.on('line', function (line) {
  if (count === 0) {
    cnt = parseInt(line);
  } else {
    let [n, m] = line.split(' ').map(Number);
    console.log(n, m);

    check++;
    if (cnt === check) rl.close();
  }

  count++;
}).on('close', function () {
  process.exit();
});
```

### Async, Await를 사용한 방법

```javascript
const readline = require('readline');

(async () => {
  let rl = readline.createInterface({ input: process.stdin });

  let count = 0;
  let cnt = 0;
  let check = 0;

  for await (const line of rl) {
    if (count === 0) {
      cnt = parseInt(line);
    } else {
      let [n, m] = line.split(' ').map(Number);
      console.log(n, m);

      check++;
      if (cnt === check) rl.close();
    }

    count++;
  }

  process.exit();
})();
```
