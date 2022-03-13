---
title: Node.js 해시 알고리즘 사용하기
date: 2022-03-13 19:05:05
tags:
  - Node.js
categories:
  - Node.js
---

## crypto

- Node.js 내장 모듈이다.

## sha256

- 외부 설치가 필요한 모듈이다.

```bash
npm install sha256
```

## 사용 예시

- 동일한 문자열을 해시화하였을 경우, crypto와 sha256의 결과가 동일한 것을 확인할 수 있다.

```javascript
const crypto = require('crypto');
const sha256 = require('sha256');

// console.log(crypto.createHash('sha256').update('My secret data').digest('base64'));
console.log(crypto.createHash('sha256').update('My secret data').digest('hex'));
console.log(sha256('My secret data'));
```

```bash
// vYkFldR7nnRtfG5x/2UMk73C/oHtvcumeyCDSZNHFNk=
bd890595d47b9e746d7c6e71ff650c93bdc2fe81edbdcba67b208349934714d9
bd890595d47b9e746d7c6e71ff650c93bdc2fe81edbdcba67b208349934714d9
```
