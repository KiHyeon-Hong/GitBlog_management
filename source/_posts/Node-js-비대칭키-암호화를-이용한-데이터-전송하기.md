---
title: Node.js 비대칭키 암호화를 이용한 데이터 전송하기
date: 2022-03-13 19:20:27
tags:
  - Node.js
categories:
  - Node.js
---

## 비대칭키 암호화를 이용한 데이터 안전하게 전송하기

- /createKey에 요청하여, 서버에서 개인키와 공개키를 생성하며, 공개키를 받아온다.
- 전송할 데이터를 공개키로 암호화하며, /useKey에 전송한다.
- 서버에서는 요청된 데이터를 개인키로 복호화한다.

## 서버 코드

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const crypto = require('crypto');
const fs = require('fs');

const app = express();
app.use(express.json());
app.use(bodyParser.urlencoded({ extended: true }));

app.get('/createKey', (req, res, next) => {
  const { publicKey, privateKey } = crypto.generateKeyPairSync('rsa', {
    modulusLength: 2048,
    publicKeyEncoding: {
      type: 'pkcs1',
      format: 'pem',
    },
    privateKeyEncoding: {
      type: 'pkcs1',
      format: 'pem',
    },
  });

  fs.writeFileSync(__dirname + '/public.pem', publicKey);
  fs.writeFileSync(__dirname + '/private.pem', privateKey);
  res.json({ publicKey: publicKey });
});

app.post('/useKey', (req, res, next) => {
  const privateKey = fs.readFileSync(__dirname + '/private.pem', 'utf8');
  const decryptedData = crypto.privateDecrypt(
    {
      key: privateKey,
      padding: crypto.constants.RSA_PKCS1_OAEP_PADDING,
      oaepHash: 'sha256',
    },
    Buffer.from(req.body.encryData, 'base64')
  );

  console.log(decryptedData.toString());
  res.send(decryptedData.toString());
});

app.listen(65001, () => {
  console.log(`Server running at 65001...`);
});
```

## 클라이언트 코드

```javascript
const request = require('request');
const fs = require('fs');
const crypto = require('crypto');

request.get('http://localhost:65001/createKey', function (error, response, body) {
  const publicKey = JSON.parse(body).publicKey;
  fs.writeFileSync(__dirname + '/public.pem', publicKey);

  const myData = 'This is secret data!';
  const encryptedData = crypto.publicEncrypt(
    {
      key: publicKey,
      padding: crypto.constants.RSA_PKCS1_OAEP_PADDING,
      oaepHash: 'sha256',
    },
    myData
  );

  const options = {
    uri: 'http://localhost:65001/useKey',
    method: 'POST',
    form: {
      encryData: encryptedData.toString('base64'),
    },
  };

  request.post(options, function (error, response, body) {
    console.log(body);
  });
});
```
