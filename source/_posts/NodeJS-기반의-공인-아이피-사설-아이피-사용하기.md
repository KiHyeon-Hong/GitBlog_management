---
title: 'NodeJS 기반의 공인 아이피, 사설 아이피 사용하기'
date: 2021-11-14 17:48:48
tags:
  - javascript
  - Node.js
categories:
  - Node.js
---

## Node.js를 이용한 공인 아이피와 사설 아이피 확인

```bash
npm i ip
npm i request
```

```javascript
const request = require('request');
const ip = require('ip');

request.get({ url: 'https://api.ipify.org' }, function (_1, _2, body) {
  console.log('Public IP address > ' + body);
  console.log('Virtual IP address > ' + ip.address());
});
```

## API를 이용하지 않는 방법

- 특정 사이트에서 가져오는 데이터는 의존성을 갖는다. 따라서, request 대신 npm 모듈을 이용한다.

```bash
npm i public-ip
```

### SyntaxError: Cannot use import statement outside a module 에러

- Node.js의 모듈은 크게 commonjs와 module로 구분할 수 있다. 이는 임포트 방식이 다르며, 이를 위해 package.json에서 module로 인식할 수 있게 변경하여야 한다.

```json
{
  ...
  "dependencies": {
    "ip": "^1.1.5",
    "public-ip": "^5.0.0",
    "request": "^2.88.2"
  },
  "type": "module"
}
```

- 다음과 같이 package.json에 "type": "module"를 추가한다.

### 임포트 방식 변경

- 이 방식으로 변경한 기존의 코드는 다음과 같다.

```javascript
import request from 'request';
import ip from 'ip';

request.get({ url: 'https://api.ipify.org' }, function (_1, _2, body) {
  console.log('Public IP address > ' + body);
  console.log('Virtual IP address > ' + ip.address());
});
```

- request 모듈을 사용하지 않는 방식은 다음과 같다.

```javascript
import publicIp from 'public-ip';
import ip from 'ip';

console.log('Public IP address > ' + (await publicIp.v4()));
console.log('Virtual IP address > ' + ip.address());
```
