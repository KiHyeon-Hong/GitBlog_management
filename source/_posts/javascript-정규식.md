---
title: Javascript 정규식
date: 2021-11-17 20:42:27
tags:
  - Javascript
categories:
  - Javascript
---

## Javascript 정규표현식

### 패턴 생성

```javascript
let pattern = /a/;
let pattern - new RegExp('a');
```

### RegExp 객체의 정규 표현식

#### RegExp.exec()

- 실행 결과는 문자열 a를 값으로 하는 배열을 리턴한다.
- a가 없다면 null을 리턴한다.
- 필요 정보 추출

```javascript
console.log(pattern.exec('abcdef')); // ['a']
console.log(pattern.exec('bcdef')); // null
```

#### RegExp.test()

- 정보가 존재하는지 확인

```javascript
console.log(pattern.test('abcdef')); // true
console.log(pattern.test('bcdef')); // false
```

### String 객체의 정규 표현식

#### String.match()

```javascript
let str = 'abcdef';
str.match(pattern); // ['a']

let str = 'bcdef';
str.match(pattern); // null
```

#### String.replace()

```javascript
let str = 'abcdef';
str.match(pattern, 'A'); // 'Abcdef'
```

### 옵션

#### i

- 대소문자를 구분하지 않는다.

```javascript
let pattern = /a/;
console.log('Abcdef'.match(pattern)); // null

let pattern = /a/i;
console.log('Abcdef'.match(pattern)); // ['A']
```

#### g

- 모든 결과를 반환한다.

```javascript
let pattern = /a/;
console.log('abcdefa'.match(pattern)); // ['a']

let pattern = /a/g;
console.log('abcdefa'.match(pattern)); // ['a', 'a']
```
