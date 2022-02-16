---
title: CommonJS와 ESModules 정리 자료3
date: 2022-02-16 22:49:25
tags:
  - Node.js
categories:
  - Node.js
---

## CommonJS and ESModules study

- Node.js에는 크게 두 종류의 스크립트가 있으며, CommonJS와 ESModules이다.
- 각각의 스크립트는 기본적으로 전혀 다르므로, npm에서 어떠한 package를 지원하는지에 따라 import, export 방법이 다르다.
- 구체적인 설명은 제외하고 node v16.13.1 LTS 기준으로 서로 간의 import 방법을 정리한다.

## Dual package

- CommonJS와 ESModules를 동시에 사용하는 패키지이다.
- 만약 라이브러리가 오직 default export만을 제공한다면, import를 사용하기만 하면 된다.

### CommonJS의 named export를 ESModules로 감싸기

- 디렉터리 구조는 다음과 같다.

![Figure1](https://kihyeon-hong.github.io/Collection_of_repository_images/CommonJS_and_ESModules_study/figure1.jpg)

- ESModules wrapper를 esm의 하위 디렉터리에 넣고, package.json에 "type"을 추가한다.

```javascript
// /esm/wrapper.js
import namedFunc from '../index.js';

export const namedSyncFunc = namedFunc.namedSyncFunc;
export const namedAsyncFunc = namedFunc.namedAsyncFunc;
```

```json
// /esm/package.json
{
  "name": "esm",
  "version": "1.0.0",
  "description": "",
  "main": "wrapper.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "type": "module"
}
```

- exports map을 추가한다.

```json
// package.json
"exports": {
    "require": "./index.js",
    "import": "./esm/wrapper.js"
}
```

### 사용 방법

#### CommonJS

```javascript
const { namedAsyncFunc, namedSyncFunc } = require('./dual/index.js');

console.log(namedSyncFunc());
(async () => {
  console.log(await namedAsyncFunc());
})();
```

#### ESModules

```javascript
import { namedAsyncFunc, namedSyncFunc } from './dual/esm/wrapper.js';

console.log(namedSyncFunc());
console.log(await namedAsyncFunc());
```

## 참고자료

- https://roseline.oopy.io/dev/translation-why-cjs-and-esm-cannot-get-along
