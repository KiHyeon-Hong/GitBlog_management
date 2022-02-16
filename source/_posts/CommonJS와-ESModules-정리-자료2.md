---
title: CommonJS와 ESModules 정리 자료2
date: 2022-02-16 22:49:15
tags:
  - Node.js
categories:
  - Node.js
---

## CommonJS and ESModules study

- Node.js에는 크게 두 종류의 스크립트가 있으며, CommonJS와 ESModules이다.
- 각각의 스크립트는 기본적으로 전혀 다르므로, npm에서 어떠한 package를 지원하는지에 따라 import, export 방법이 다르다.
- 구체적인 설명은 제외하고 node v16.13.1 LTS 기준으로 서로 간의 import 방법을 정리한다.

## ESModules

### ESModules에서 ESModules 불러오기

- ESModules은 하나의 파일안에 named export와 default export를 사용할 수 있다.
- named export를 불러오기 위해, 객체 구조 분해 연산을 이용하며, default export를 불러오기 위해 변수를 지정한다. 지정된 변수명으로 default export의 메소드를 호출할 수 있다.

```javascript
/*
 * /index.js
 */
const promise = () => {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve('This is async...');
    }, 3000);
  });
};

export async function namedAsyncFunc() {
  return promise();
}

export function namedSyncFunc() {
  return 'This is sync...';
}

export default function defaultFunc() {
  return 'This is default...';
}

/*
 * index.js
 */
import { namedAsyncFunc, namedSyncFunc } from './esm/index.js';
import defaultFunc from './esm/index.js';

console.log(namedSyncFunc());
console.log(await namedAsyncFunc());
console.log(defaultFunc());
```

```bash
This is sync...
This is async...
This is default...
```

### ESModules에서 CommonJS 불러오기

- ESModules에서 CommonJS를 불러오는 것은 import로도 가능하다. (require 사용 불가능)
- 이는 ESModules를 호출할 때와 같으며, ESModules는 Top-Level Await를 지원하기 때문에 async 메소드 없이 await를 사용할 수 있다.
- 추가적으로 객체 구조 분해 연산 뿐만이 아니라, 변수명을 지정하여 named export를 이용할 수 있으며, 이 경우에는 변수명.메소드명()으로 named export를 이용한다.

```javascript
/*
 * /default/index.js
 */
module.exports = () => {
  return 'This is default...';
};

/*
 * /named/index.js
 */
const promise = () => {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve('This is async...');
    }, 3000);
  });
};

module.exports.namedAsyncFunc = async () => {
  return promise();
};

module.exports.namedSyncFunc = () => {
  return 'This is sync...';
};

/*
 * index.js
 */
import defaultFunc from './cjs/default/index.js';
import { namedSyncFunc, namedAsyncFunc } from './cjs/named/index.js';

console.log(namedSyncFunc());
console.log(await namedAsyncFunc());
console.log(defaultFunc());

console.log();
console.log('==============================');
console.log();

import namedFunc from './cjs/named/index.js';

console.log(namedFunc.namedSyncFunc());
console.log(await namedFunc.namedAsyncFunc());
```

```bash
This is sync...
This is async...
This is default...

==============================

This is sync...
This is async...
```

### ESModules에서 불러온 ESModules 타입

- ESModules의 타입은 [형식 : 이름] 형태로 반환된다.
- promise와 같은 비동기적으로 반환되는 메소드는 AsyncFunction이며, 동기적으로 반환되는 메소드는 Function이다.

```javascript
/*
 * /index.js
 */
const promise = () => {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve('This is async...');
    }, 3000);
  });
};

export async function namedAsyncFunc() {
  return promise();
}

export function namedSyncFunc() {
  return 'This is sync...';
}

export default function defaultFunc() {
  return 'This is default...';
}

/*
 * index.js
 */
import { namedAsyncFunc, namedSyncFunc } from './esm/index.js';
import defaultFunc from './esm/index.js';

console.log(namedSyncFunc); // [Function: namedSyncFunc]
console.log(namedAsyncFunc); // [AsyncFunction: namedAsyncFunc]
console.log(defaultFunc); // [Function: defaultFunc]
```

```bash
[Function: namedSyncFunc]
[AsyncFunction: namedAsyncFunc]
[Function: defaultFunc]
```

### 다양한 방법으로 ESModules 불러오기

#### import 줄여쓰기

- default export와 named export는 하나의 import 문으로 불러올 수 있다.

```javascript
import defaultFunc, { namedSyncFunc, namedAsyncFunc } from './esm/index.js';

console.log(namedSyncFunc());
console.log(await namedAsyncFunc());
console.log(defaultFunc());
```

```bash
This is sync...
This is async...
This is default...
```

#### 별명 붙이기

- 구조 분해 할당 연산을 이용할 경우 불러오는 named export에 별명을 붙일 수 있으며, default export에 별명을 붙이기 위해서는 구조 분해 할당 연산 안에서 default로 불러올 수 있다.

```javascript
import { namedSyncFunc as sf, namedAsyncFunc as af, default as df } from './esm/index.js';

console.log(sf());
console.log(await af());
console.log(df());
```

```bash
This is sync...
This is async...
This is default...
```

#### 모두 불러오기

- '\*'을 이용하여 모든 named export와 default export를 불러올 수 있으며, 이 경우에는 default export를 불러오기 위해 default()를 이용하여야 한다.
- 불러온 모듈의 타입은 CommonJS에서 EXModules를 불러왔을 경우와 동일하다.

```javascript
import * as f from './esm/index.js';

console.log(f);

console.log(f.namedSyncFunc());
console.log(await f.namedAsyncFunc());
console.log(f.default());
```

```bash
[Module: null prototype] {
  default: [Function: defaultFunc],
  namedAsyncFunc: [AsyncFunction: namedAsyncFunc],
  namedSyncFunc: [Function: namedSyncFunc]
}
This is sync...
This is async...
This is default...
```

## 참고자료

- https://roseline.oopy.io/dev/translation-why-cjs-and-esm-cannot-get-along
