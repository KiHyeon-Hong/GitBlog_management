---
title: 'Javascript Async, Await 공부'
date: 2021-11-26 14:23:46
tags:
  - javascript
  - Promise
  - Asynchronous
categories:
  - Javascript
  - Asynchronous
---

- http://junil-hwang.com/blog/javascript-promise-async-await/

## Async, Await 간단 설명

- async, await는 비동기로 실행되는 것을 끝날 때까지 기다리는 방법 (동기처럼 사용)
- async, await를 사용하기 위해 Promise를 사용한다.

## 간단한 Promise 코드 작성

- promise는 Promise 객체를 반환하며, 1초 후 입력받은 값에 1을 더한 값을 반환한다.

```javascript
const cnt0 = 0;
const promise = (v) => {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve(v + 1);
    }, 1000);
  });
};
```

## Async, Await를 사용하지 않은 Promise

- 기존의 비동기를 사용하듯이 promise를 사용하는 방법
- 무한 callback에 빠진다.

```javascript
promise(cnt0).then((cnt1) => {
  console.log(cnt1);
  promise(cnt1).then((cnt2) => {
    console.log(cnt2);
    promise(cnt2).then((cnt3) => {
      console.log(cnt3);
    });
  });
});
```

- 적절한 체이닝을 이용하여 promise를 조작하는 방법
- 비동기라는 특성에서 완전히 벗어나지는 못한다.

```javascript
promise(cnt0)
  .then((cnt1) => {
    console.log(cnt1);
    return promise(cnt1);
  })
  .then((cnt2) => {
    console.log(cnt2);
    return promise(cnt2);
  })
  .then((cnt3) => {
    console.log(cnt3);
  });
```

## Async, Await를 사용한 Promise

- Promise를 반환하는 함수의 앞에 await를 사용한다.
- await를 사용하는 함수 앞에는 async라는 키워드를 사용한다.
- resolve의 인자가 await 구문으로 반환된다.

```javascript
(async () => {
  const cnt1 = await promise(cnt0);
  console.log(cnt1);
  const cnt2 = await promise(cnt1);
  console.log(cnt2);
  const cnt3 = await promise(cnt2);
  console.log(cnt3);
})();
```
