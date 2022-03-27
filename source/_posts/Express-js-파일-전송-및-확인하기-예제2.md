---
title: Express.js 파일 전송 및 확인하기 예제2
date: 2022-03-27 14:14:31
tags:
  - Node.js
categories:
  - Node.js
---

## 개요

- https://kihyeon-hong.github.io/2022/03/27/Express-js-파일-전송-및-확인하기-예제1/
- 기존의 예제를 응용하여, 서버로 파일을 전송하고, 목록을 확인하여 전송한 파일을 볼 수 있는 간단한 문서 뷰어를 구현한다.

## 필요 모듈 설치

```bash
npm i express
npm i body-parser
npm i multer
npm i ejs
```

## 문서 뷰어 웹페이지 소스 코드 구현

### index.js

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const multer = require('multer');
const fs = require('fs');

const app = express();

app.use(express.json());
app.use(bodyParser.urlencoded({ extended: false }));
app.use('/files', express.static('files'));

app.set('view engine', 'ejs');

var storage = multer.diskStorage({
  destination: function (req, file, cb) {
    cb(null, './files');
  },
  filename: function (req, file, cb) {
    cb(null, file.originalname);
  },
});

const upload = multer({ storage: storage });

app.get('/', (req, res, next) => {
  res.render('index', {
    files: fs.readdirSync('files'),
  });
});

app.get('/files', (req, res, next) => {
  res.send(fs.readFileSync(`files/${req.query.name}`, 'utf8'));
});

app.post('/upload', upload.single('mydata'), (req, res) => {
  console.log(req.file);
  res.redirect(['/']);
});

app.listen(65001, () => {
  console.log(`Server running 65001...`);
});
```

### views/index.ejs

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
  </head>
  <body>
    <form action="upload" method="post" enctype="multipart/form-data">
      <input type="file" name="mydata" />
      <input type="submit" value="저장" />
    </form>

    <br />

    <% for(let i = 0; i < files.length; i++) { %>
    <form action="files" method="get">
      <input type="text" value="<%= files[i] %>" name="name" readonly />
      <input type="submit" value="보기" />
    </form>
    <% } %>
  </body>
</html>
```

### files/test.html

```html
<!DOCTYPE html>
<html>
  <head> </head>
  <body>
    <h3>Test!!!</h3>
  </body>
</html>
```

```bash
node index.js
```

## 테스트

<p align="center"><img src="/images/Node_js/Express/Multer/FileViewer/FileViewer1.jpg"></p>

- 처음 웹 페이지를 접속하면, 기본적으로 작성해둔 test.html을 확인할 수 있다.

<p align="center"><img src="/images/Node_js/Express/Multer/FileViewer/FileViewer2.jpg"></p>

- 해당 파일을 열어보면 다음과 같이 나타난다.

<p align="center"><img src="/images/Node_js/Express/Multer/FileViewer/FileViewer3.jpg"></p>

- 새로운 파일을 첨부하고 저장을 누른다.

<p align="center"><img src="/images/Node_js/Express/Multer/FileViewer/FileViewer4.jpg"></p>

- 추가한 파일이 나타난다.

<p align="center"><img src="/images/Node_js/Express/Multer/FileViewer/FileViewer5.jpg"></p>

- 추가한 파일을 열어보면 다음과 같이 해당 파일의 내용을 확인할 수 있다.
