---
title: 'Javascript promise, async, 그리고 await 공부1'
date: 2022-02-08 14:17:54
tags:
  - javascript
  - Promise
  - Asynchronous
categories:
  - Javascript
  - Promise
---

## Javascript promise, async, and await study

### State

- Pending -> Fulfilled or Rejected
- Pending: 이행하지도, 거부하지도 않은 상태
- Fulfilled: 연산이 성공적으로 완료됨
- Rejected: 연산이 실패함

### Producer and Consumers

- Promise를 생성할 때, 2개의 callback을 받는데, Resolve와 Reject이다.
- Promise는 생성되는 순간에 executer라는 callback 함수가 실행된다.

```javascript
// 호출을 하지 않았지만, Promise가 생성됨과 동시에 실행되어 console.log가 출력된다.
const promise = new Promise((resolve, reject) => {
  console.log('doing something');
});
```

- Promise는 Resolve나 Reject를 호출하지 안으면, 언제까지나 Pending 상태로 남아있다.
- Promise는 Promise를 리턴하기 때문에 then, catch, finally 등을 사용하여 값을 출력한다.

```javascript
// 1. Producer
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('good!');
  }, 1000);
});

// 2. Consumers: then, catch, finally
promise.then((value) => {
  console.log(value);
});
```

### Chaining

- Then은 Promise를 반환하기 때문에 다시 catch를 호출할 수 있다.
- 이때, then은 값(data)를 전달할 수 있으며, promise를 전달할 수도 있다.
- 추가적으로 finally는 성공과 실패 여부와 상관없이 실행된다.

```javascript
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject(new Error('network Error!'));
  }, 2000);
});

promise
  .then((value) => {
    console.log(value);
  })
  .catch((error) => {
    console.log(error);
  })
  .finally(() => {
    console.log('finally');
  });
```

```bash
Error: network Error!
    at Timeout._onTimeout (C:\Users\ghdrl\Desktop\Temp\Code\Study\JavaScript\AsyncAwaitStudy\test.js:3:12)
    at listOnTimeout (node:internal/timers:557:17)
    at processTimers (node:internal/timers:500:7)
finally
```

#### Promise or data 전달 예제

```javascript
const feachNumber = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve(1);
  }, 1000);
});

feachNumber // Promise 전달
  .then((num) => num * 2) // 값 전달
  .then((num) => num * 3) // 값 전달
  .then((num) => {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve(num - 1);
      }, 1000);
    });
  }) // Promise 전달
  .then((num) => console.log(num));
// 2000ms 뒤 5 출력
```

### Parameter 생략

- 만약, parameter를 함수에 그대로 넣어준다면, 식의 생략이 가능하다.

```javascript
const add1 = (num) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(num + 1);
    }, 1000);
  });
};

const add2 = (num) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(num + 2);
    }, 1000);
  });
};

const add3 = (num) => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve(num + 3);
    }, 1000);
  });
};

add1(10)
  .then((sum) => add2(sum))
  .then((sum) => add3(sum))
  .then((sum) => {
    console.log(sum);
  });

// Parameter 생략
add1(10) //
  .then(add2)
  .then(add3)
  .then(console.log)
  .catch(console.log);
```
