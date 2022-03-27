---
title: Express.js 파일 전송 및 확인하기 예제1
date: 2022-03-27 14:14:22
tags:
  - Node.js
categories:
  - Node.js
---

## 필요 모듈 설치하기

```bash
npm i express
npm i body-parser
npm i multer
```

## 소스코드 작성하기

```javascript
const bodyParser = require('body-parser');
const multer = require('multer');

const express = require('express');
const app = express();

app.use(express.json());
app.use(bodyParser.urlencoded({ extended: false }));
app.use('/myimages', express.static('images'));

var storage = multer.diskStorage({
  destination: function (req, file, cb) {
    // cb 콜백함수를 통해 전송된 파일 저장 디렉토리 설정
    cb(null, './images');
  },
  filename: function (req, file, cb) {
    // cb 콜백함수를 통해 전송된 파일 이름 설정
    cb(null, file.originalname);
    // cb(null, 'test.jpg');
  },
});

// const upload = multer({dest: './images/'});
const upload = multer({ storage: storage });

app.post('/upload', upload.single('img'), (req, res) => {
  console.log(req.file);
  res.json(req.file);
});

app.listen(65001, () => {
  console.log('server running start');
});
```

```bash
node index.js
```

## 파일 전송 예제

- Postman을 이용하여 서버로 이미지를 전송한다.

<p align="center"><img src="/images/Node_js/Express/Multer/ImageQuery/ImageQuery1.jpg"></p>

- 전송 시, 파일에 대한 정보가 반환되는 것을 볼 수 있다.

<p align="center"><img src="/images/Node_js/Express/Multer/ImageQuery/ImageQuery2.jpg"></p>

## 전송 파일 확인하기

- 서버에 저장된 이미지 파일을 확인하기 위해, 웹 브라우저에 다음과 같이 입력한다.
- 이때, test.png는 서버로 전송한 이미지 파일 이름이다.

```text
http://localhost:65001/myImages/test.png
```

<p align="center"><img src="/images/Node_js/Express/Multer/ImageQuery/ImageQuery3.jpg"></p>
