---
title: Javascript 정규표현식 정리2
date: 2022-01-28 12:03:59
tags:
  - javascript
categories:
  - Javascript
---

## 자바스크립트 정규표현식 메소드

- exec: 대응되는 문자열을 찾는 RegExp 메소드, 정보를 가지고 있는 배열을 반환하며, 대응되는 문자열이 없을 경우 null을 반환
- test: 대응되는 문자열이 있는지 검사하는 RegExp 메소드, true or false
- match: 대응되는 문자열을 찾는 string 메소드, 정보를 가지고 있는 배열을 반환하며, 대응되는 문자열이 없을 경우 null을 반환
- search: 대응되는 문자열이 있는지 검사하는 string 메소드, 대응되는 부분의 인덱스를 반환, 없다면 -1
- replace: 대응되는 문자열을 찾아 다른 문자열로 치환하는 string 메소드
- split: 정규식 혹은 문자열로 대상 문자열을 나누어 배열로 반환하는 string 메소드

```javascript
var myRe = /d(b+)d/g;
console.log(myRe.exec('cdbbdbsbz'));
console.log(/d(b+)d/g.exec('cdbbdbsbz'));

// 문자열로 표현한 형식!
myRe = new RegExp('d(b+)d', 'g');
console.log(myRe.exec('cdbbdbsbz'));
```

- index: 입력된 문자열에서 대응된 부분에 해당하는 인덱스
- input: 입력된 원본 문자열
- [0]: 마지막으로 대응된 문자열

- lastIndex: 다음 검색 시 시작할 인덱스(g 옵션을 설정한 정규식에서만 가능)
- source: 패턴 문자열

```javascript
var myRe = /d(b+)d/g;
var myArray = myRe.exec('cdbbdbsbz');
console.log('The value of lastIndex is ' + myRe.lastIndex);
```

## 괄호로 둘러 싼 패턴 사용하기

```javascript
var re = /(\w+)\s(\w+)/;
var str = 'John Smith';
var newstr = str.replace(re, '$2, $1');

console.log(re.exec(str));
console.log(newstr);
```

## 플래그

- g: 전역 검색
- i: 대소문자 구분 없는 검색
- m: 다중행 검색
- s: .에 개행 문자도 매칭
- u: 유니코드, 패턴을 유니코드 코드 포인트의 나열로 취급
- y: "sticky"검색을 수행. 문자열의 현재 위치부터 검색을 수행

```javascript
var re = /\w+\s/g;
var str = 'fee fi fo fum';
var myArray = str.match(re);

console.log(myArray);
```

- var re = /\w+\s/g;
- var re = new RegExp("\\w+\\s", "g");
- 이 둘은 동일하다.

- str.match(re)
- re.exec(str)
- match와 exec는 사용방법이 다르다

```javascript
var xArray;
while ((xArray = re.exec(str))) console.log(xArray);

console.log();
console.log(re.exec(str));
console.log(re.exec(str));
console.log(re.exec(str));
console.log(re.exec(str));
console.log(re.exec(str));
console.log(re.exec(str));
console.log(re.exec(str));
console.log(re.exec(str));
console.log();
```

- m 플래그는 여러 줄의 입력 문자열이 실제로 여러 줄로 다뤄져야 하는 경우에 사용함
- 만약 m 플래그가 사용되면 ^, $ 문자는 전체 문자열의 시작과 끝에 대응되지 않고, 각 라인의 시작과 끝에 대응됨
