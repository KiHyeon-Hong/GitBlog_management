---
title: 'Javascript async, await와 반복문'
date: 2022-02-08 14:28:25
tags:
  - javascript
  - Promise
  - Asynchronous
categories:
  - Javascript
  - Promise
---

## Async, Await와 반복문

### 주의사항

- Promise는 생성과 동시에 동작하고, pending 상태에서 fulfilled나 rejected 상태를 기다린다.
- fulfilled나 rejected 상태가 된다면, await나 then, catch 등을 이용하여 promise의 반환값을 즉시 받아올 수 있다.
- 따라서 다음과 같이 코드를 작성하면, 첫 반복문에서 promise가 1,000ms 기다린 후 로그가 출력되지만, 다음 반복문 부터, 이미 완료된 promise에서 값을 받아오기 때문에 1,000ms의 기다림 없이 즉시 실행된다.(network1은 1000ms후 fulfilled 상태가 되기 때문에, 처음 반복문 1회를 제외하고 기다릴 필요가 없다.)

```javascript
const network1 = new Promise((resolve) => {
  setTimeout(() => resolve('Success!'), 1000);
});

async function main() {
  for (let i = 0; i < 10; i++) {
    console.log(await network1);
  }
}

main();
```

- 이를 해결하기 위해 1,000ms마다 딜레이를 주고 싶다면, promise를 함수로 리턴한 후, 매 반복문 마다 새로운 promise를 생성하고 동작시켜야 한다.

```javascript
const network2 = () => {
  return new Promise((resolve) => {
    setTimeout(() => resolve('Success!'), 1000);
  });
};

async function main() {
  for (let i = 0; i < 10; i++) {
    console.log(await network2());
  }
}

main();
```
