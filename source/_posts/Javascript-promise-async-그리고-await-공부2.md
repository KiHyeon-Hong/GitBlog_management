---
title: 'Javascript promise, async, 그리고 await 공부2'
date: 2022-02-08 14:23:46
tags:
  - javascript
  - Promise
  - Asynchronous
categories:
  - Javascript
  - Promise
---

## Javascript promise, async, and await study

### Async

- 함수 앞에 async를 붙여주면 코드 블록이 Promise로 변화한다.

```javascript
async function fetchUser() {
  return 'Good?';
}

console.log(fetchUser());
// Promise { 'Good?' }
```

### Await

- await는 async가 붙은 함수 내에서만 사용할 수 있다.

```javascript
function sleep(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}

async function getNum100() {
  await sleep(3000);
  return 100;
}

async function getNum200() {
  await sleep(3000);
  return 200;
}

async function getNum300() {
  const num300 = (await getNum100()) + (await getNum200());
  return num300;
}

// 6000ms 뒤 300 출력
(async () => {
  console.log(await getNum300());
})();
```

### Await 병렬 연결하기

- 위 예졔는 하나의 await가 종료된 후에야 다음 await를 기다리기 때문에 6,000ms의 시간이 소요된다.
- 이를 해결하는 방법은 두 promise문을 동시에 실행할 수 있다.
- all(): 모든 promise가 끝나면 결과를 배열로 반환한다.
- race(): 가장 먼저 끝난 promise 결과 하나를 받아온다.

```javascript
function sleep(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}

async function getNum100() {
  await sleep(3000);
  return 100;
}

async function getNum200() {
  await sleep(3000);
  return 200;
}

async function getNum300() {
  return Promise.all([getNum100(), getNum200()]).then((datas) => {
    return datas.reduce((p, v) => {
      return p + v;
    }, 0);
  });
}

// 3000ms 뒤 300 출력
(async () => {
  console.log(await getNum300());
})();
```
