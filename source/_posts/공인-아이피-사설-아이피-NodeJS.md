---
title: '공인 아이피, 사설 아이피 NodeJS'
date: 2021-11-14 17:48:48
tags:
    - Javascript
    - Node.js
categories:
    - Node.js
---

### Node.js를 이용한 공인 아이피와 사설 아이피 확인

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
