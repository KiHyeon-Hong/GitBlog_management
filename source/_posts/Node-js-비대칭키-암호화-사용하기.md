---
title: Node.js 비대칭키 암호화 사용하기
date: 2022-03-13 19:05:50
tags:
  - Node.js
categories:
  - Node.js
---

## 비대칭키 암호화 알고리즘 예시

- crypto 내장 모듈을 이용한 비대칭키 암호화 알고리즘을 사용한다.

```javascript
const crypto = require('crypto');
const fs = require('fs');

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

const data = 'My secret data';

const encryptedData = crypto.publicEncrypt(
  {
    key: publicKey,
    padding: crypto.constants.RSA_PKCS1_OAEP_PADDING,
    oaepHash: 'sha256',
  },
  data
);

const decryptedData = crypto.privateDecrypt(
  {
    key: privateKey,
    padding: crypto.constants.RSA_PKCS1_OAEP_PADDING,
    oaepHash: 'sha256',
  },
  encryptedData
);

console.log('encypted data: ', encryptedData.toString('base64'));
console.log('decrypted data: ', decryptedData.toString());

fs.writeFileSync('./public.pem', publicKey);
fs.writeFileSync('./private.pem', privateKey);
```

- 출력 결과는 다음과 같다.

```bash
encypted data:  eae/p7QrC2SePZMbHGPb1SYjkK3CIbdeoFwTXQ/bozinpyJONGPVAT4333unFb80mp2grZ7ZdySnXvcH7vIAkRsc5jBPoHqszoWFLAitWv6djDiZrmD/azI0U7d0bFcoKDpa2jjCt19V4leDG58ROwxSDvAIJ1KB6zvyhIf+1GghG0FKjXS64hwIN+noAW6cBZqKREhPULP/ayG8H0lFpK5WHFNWmgbxIwFvEK3tKqhj+N+cCy2dCxRV/jDbeOrjVdt4UHv3lC5F6LVX4q0hDGQHWmD2AFpduBhYa7sZ9S59haMZ7/4PGUq01TyCTA/bH1PZuJgUWLqRyeaoujXXRQ==
decrypted data:  My secret data
```

## 공개키, 개인키 파일

- 저장된 공개키 파일은 다음과 같다

```text
-----BEGIN RSA PUBLIC KEY-----
MIIBCgKCAQEAuXFoJvFMZ98kRrYXYjA0B/giRYis5qrbYmlHaZ1n3mXdtZzclsqM
QwiPLwZAYgICNNHwqaehTEUTVuMyk4Zo8IuL+hY2UJBXYjodTFoVruJlWr+mio+r
jUXi6VZLpEBdyIjq3WKrxzIhCK10juAUqTOh7NS+JGFZA+Npo0k8rf3TQXtaebsn
wvovmcZvGJOgUkflfY03B2QBjvYTc8DI67y69n6a5LeoH8hbBcbM4STkv2k+wIuN
uEURb8DTaLdbp45wgKWrE4Wk4eEaKvueXCDGMF2tVkZEsZqgQceosJcp2Uvs5NFj
6xF6Co+f/fTJcen03cggzMjpjMCXzYpArQIDAQAB
-----END RSA PUBLIC KEY-----
```

- 저장된 개인키 파일은 다음과 같다.

```text
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAuXFoJvFMZ98kRrYXYjA0B/giRYis5qrbYmlHaZ1n3mXdtZzc
lsqMQwiPLwZAYgICNNHwqaehTEUTVuMyk4Zo8IuL+hY2UJBXYjodTFoVruJlWr+m
io+rjUXi6VZLpEBdyIjq3WKrxzIhCK10juAUqTOh7NS+JGFZA+Npo0k8rf3TQXta
ebsnwvovmcZvGJOgUkflfY03B2QBjvYTc8DI67y69n6a5LeoH8hbBcbM4STkv2k+
wIuNuEURb8DTaLdbp45wgKWrE4Wk4eEaKvueXCDGMF2tVkZEsZqgQceosJcp2Uvs
5NFj6xF6Co+f/fTJcen03cggzMjpjMCXzYpArQIDAQABAoIBAG3si5CJ+ICaBSbl
SXcqm60dqTMOkW8qWGE9htdUNv3d5E6DbT71Ua9qo3V8fy2ZgzVMPRxUAYj0aUJX
6uMICayNC6xy/j9DUIkpabSYscG48duZP19jSo2zn44xWSVEAlOc1ZvloW2yiWJb
b3xB1/10XcfFU/C8w8dKRpREFXQMv5qYFqZchq2WU3iVSDpivIXW2Ee/Kxs/eWh3
BCnb/J6tpFBa9oqt/eS1SohKQuJ9Zcea6qukTwv3RsSrnNOGCyCeJWoqddaL0hCH
sRrtvn+02/J8t6FOrfXEytM/Vobdq+NivrpGXSfXmJksG6PKBFZted/7joSiMj73
sCRLCAECgYEA2/O0qG7JuFppnOQc8BJxomGKt6gWzJiy1XaK/ufiCwVOIXA22PTL
OBKJrSZ8n8a2y4odzO+vlq408nMgP63nWB+zu99PdIi6g6FRAHLsVPX0p12UBsZn
0DYnte1hxPJ1kZgejTpxtxjTENXY7+MWpYnZEx+5CBZ+XD4VgYhug3UCgYEA19XY
FZXIOp+fU8Vrfn+7/UBSR1vYWPd6oX/ZSKBS4+R3b8jrxXwf1ZHB8+XmkgcHI0wQ
fZTfX7xrhDuOpJrzqQWvOdjnFTey0p7dRO5C/nNUbQJIUZfXL0lZL1ZwlGncGAlp
CXAjofkeWveHhqtHT/nfbhhh38ZrFigDV+DDuVkCgYBHo+851Sv60egIY/xQ7ZD5
lM+71hHm/e1xvbS0Jg7oDAhQt94FeGYgk1kofpqk5/JuBUSDlaYZbBBuz7S3SQtL
FrhR/wBAMrCdYxOhE82KNrpDMSWft0vk816n0PPBVD+a9nMtCNY1Du7gUubf65Va
wbVklzaLPdhWbxpOIIPuaQKBgEvZS5myTG5FoCE5VKBc1TyXeRK4tRv2xHKy0jIS
nW6W4F45VpnNGAbetTE4DsIslBaUaYsoYSNsvL/4ihVQmuZAKCcFEZhEPaSEza+m
p4ZyEy5HyhBacvWcKipXjzKozP7pd68oaG1IdaF0MX1i/ameXyV6jhKs0P81So98
XmvpAoGAajtrMPz48KnlAk+vFtA6i1E85k25rHf9WMTItv/N4iRvkYYBlEkXwgg6
nKlDX71llcYFCm9s509KbjeKWLt68XE+lDvuAPL0ippvndpfhUAiJgD5NM2YI1/e
iWqq3/B8k4FIGqh9h44cJX2eoxFxYrHc2tEJcBU1Ma5D8AuHBKs=
-----END RSA PRIVATE KEY-----
```
