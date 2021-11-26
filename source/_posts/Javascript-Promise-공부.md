---
title: Javascript Promise 공부
date: 2021-11-26 14:12:54
tags:
  - Javascript
  - Promise
  - Asynchronous
categories:
  - Javascript
  - Promise
---

- 출처: https://github.com/azu
- 한빛출판네트워크, JavaScript Promise에서 중요 부분만 발췌

## Promise.prototype.then

- promise.then(onFulfilled, onRejected);

```javascript
var promise = new Promise(function (resolve, reject) {
  resolve('이 값은 then()에 전달된다.');
});
promise.then(
  function (value) {
    console.log(value);
  },
  function (error) {
    console.error(error);
  }
);
```

- promise 객체에 대한 onFulfilled와 onRejected 콜백 함수를 정의하고 새로운 promise 객체를 반환한다. 이 함수는 promise 객체가 완료resolve 또는 실패reject될 때 각각 호출된다. 처리 로직에서 반환한 값은 새로운 promise 객체의 onFulfilled 콜백 함수에 전달한다. 처리 로직에서 오류가 발생하면 error 객체를 새로운 promise 객체의 onRejected 콜백 함수에 전달한다.

## Promise.prototype.catch

- promise.catch(onRejected);

```javascript
var promise = new Promise(function (resolve, reject) {
  reject(new Error('error 객체는 catch()에 전달된다.'));
});
promise
  .then(function (value) {
    console.log(value);
  })
  .catch(function (error) {
    console.error(error);
  });
```

## Promise.resolve

- Promise.resolve(promise);
- Promise.resolve(thenable);
- Promise.resolve(object);

```javascript
var taskName = 'task 1';
asyncTask(taskName)
  .then(function (value) {
    console.log(value);
  })
  .catch(function (error) {
    console.error(error);
  });
function asyncTask(name) {
  return Promise.resolve(name).then(function (value) {
    return 'Done! ' + value;
  });
}
```

- Fulfilled 상태의 promise 객체를 반환한다. 전달받은 값은 then()으로 등록한 콜백 함수에 전달된다. 어떤 경우에도 promise 객체를 반환하지만 크게 세 가지 케이스로 나눌 수 있다.
  ● promise 객체를 전달받은 경우엔 전달받은 객체를 반환한다.
  ● thenable 객체를 전달받은 경우엔 promise 객체로 변환해서 반환한다.
  ● 다른 값(객체나 null 포함)을 전달받은 경우엔 새로운 promise 객체를 생성해 반환한다.

## Promise.reject

- Promise.reject(object)

```javascript
var r = Promise.reject(new Error('error'));
console.log(r === Promise.reject(r)); // false
```

- Rejected 상태의 promise 객체를 생성해 반환한다. reject()에는 error 객체를 전달해야 한다. 전달받은 값은 catch()로 등록한 콜백 함수에 전달된다. resolve()와는 달리 항상 새로운 객체를 생성한다.

## Promise.all

- Promise.all(promiseArray);

```javascript
var p1 = Promise.resolve(1),
  p2 = Promise.resolve(2),
  p3 = Promise.resolve(3);
Promise.all([p1, p2, p3]).then(function (results) {
  console.log(results); // [1, 2, 3]
});
```

- 새로운 promise 객체를 생성해 반환한다. 배열로 전달한 promise 객체의 처리가 모두 완료됐을 때 새로운 promise 객체도 완료된다. 객체 중 하나라도 실패하면 새로운 객체도 실패한다. 배열의 값은 Promise.resolve()로 다뤄지기 때문에 promise 객체 이외의 값이 존재해도 정상적으로 동작한다.

## Promise.race

- Promise.race(promiseArray);

```javascript
var p1 = Promise.resolve(1),
  p2 = Promise.resolve(2),
  p3 = Promise.resolve(3);
Promise.race([p1, p2, p3]).then(function (value) {
  console.log(value); // 1
});
```

- 새로운 promise 객체를 생성해 반환한다. 배열로 전달한 promise 객체 중 하나만 완료되면 새로운 promise 객체도 완료된다.
