---
title: 'Javascript call, apply, 그리고 bind 공부'
date: 2021-11-26 15:06:21
tags:
  - Javascript
categories:
  - Javascript
---

- https://www.youtube.com/watch?v=KfuyXQLFNW4&list=PLZKTXPmaJk8JZ2NAC538UzhY_UNqMdZB4&index=13

## Call

- 모든 함수에서 사용할 수 있으며, this를 특정한 값으로 지정한다.

```javascript
const mike = {
  name: 'Mike',
};
const tom = {
  name: 'Tom',
};

function showThisName() {
  console.log(this.name);
}

showThisName(); // error
showThisName.call(mike); // Mike
```

- 첫 번째 매개 변수는 this로 사용할 값이며, 나머지 뒤의 매개 변수는 함수의 파라매터

```javascript
function update(birthYear, occupation) {
  this.birthYear = birthYear;
  this.occupation = occupation;
}

update.call(mike, 1999, 'singer');
```

## Apply

- 함수의 매개변수를 처리하는 방법을 제외하면 call과 완전히 동일하다.
- call은 일반적인 함수와 마찬가지로 매개 변수를 직접 받지만, apply는 매개변수를 배열로 받는다.

```javascript
update.apply(mike, [1999, 'singer']);

const num = [3, 2, 1, 5, 4];

// 동일한 결과를 갖는다.
const min = Math.min(...num);
const min = Math.min.apply(null, num);
const min = Math.min.call(null, ...num);
```

## Bind

- 함수의 this 값을 영구히 바꾼다.

```javascript
const updateMike = update.bind(mike);
updateMike(mike);
```
