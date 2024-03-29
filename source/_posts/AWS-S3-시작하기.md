---
title: AWS S3 시작하기
date: 2020-10-06 13:30:55
tags:
  - S3
  - AWS
categories:
  - AWS
thumbnail: /images/AWS/AWSGuide/S3_시작하기/index.svg
---

<p align="center"><img src="/images/AWS/AWSGuide/S3_시작하기/index.svg"></p>

S3은 어디서나 원하는 양의 데이터를 저장하고 검색할 수 있도록 구축된 객체 스토리지이다.

---

- S3은 스토리지 형식으로 객체 스토리지를 사용한다.
- 계층 구조가 없고, 고유식별 번호와 데이터 그리고 메타 데이터 등 최소한의 정보만을 가지고 있기 때문에 파일 개수가 많아져도 파일 스토리지에 비해 훨씬 많은 수의 파일들을 처리할 수 있다.
- 높은 내구성
- 손쉬운 혹장성
- 보안성과 편리성
- 관리 유연성

---

<부트 스토립을 이용한 반응형 페이지 생성 실습>

1. 부트스트랩 홈페이지 접속
2. 부트스트랩 템플릿 다운로드
3. S3버킷 생성
4. 부트스트랩 템플릿 파일 업로드
5. 정적 웹 사이트 설정
6. 엔드포인트 URL을 통한 부트스트랩 index.html 확인

---

<p align="center"><img src="/images/AWS/AWSGuide/S3_시작하기/S3Start.jpg"></p>

- AWS 콘솔에서 스토리지 서비스인 S3을 검색한다.

<p align="center"><img src="/images/AWS/AWSGuide/S3_시작하기/S3Start1.jpg"></p>

- 다음과 같은 화면이 나오면 버킷 만들기를 클릭한다.

<p align="center"><img src="/images/AWS/AWSGuide/S3_시작하기/S3Start2.jpg"></p>

- 버킷 이름과 리전을 선택한다.
- 이 때, 버킷 이름은 저세계에서 유일해야 하며, 리전은 Educate 버전 사용 시 버지니아 북부로 해야 한다.

<p align="center"><img src="/images/AWS/AWSGuide/S3_시작하기/S3Start3.jpg"></p>

- 옵션은 기본으로 설정하고 넘어간다.

<p align="center"><img src="/images/AWS/AWSGuide/S3_시작하기/S3Start4.jpg"></p>

- 모든 퍼블릭 엑세스 차단을 해제한다.
- 차단을 해제 하여야 외부 사람이 접근 가능하다.

<p align="center"><img src="/images/AWS/AWSGuide/S3_시작하기/S3Start5.jpg"></p>

- 검토 후 문제가 없다면 버킷 만들기를 선택한다.

---

<p align="center"><img src="/images/AWS/AWSGuide/S3_시작하기/S3Start6.jpg"></p>

- 버킷이 새로 만들어 졌다.

<p align="center"><img src="/images/AWS/AWSGuide/S3_시작하기/S3Start7.jpg"></p>

- 새로 새성한 버킷을 선택하면 다음과 같은 화면이 출력된다.

---

<p align="center"><img src="/images/AWS/AWSGuide/S3_시작하기/S3Start8.jpg"></p>

- https://startbootstrap.com/
- 부트스트랩을 이용한 반응형 웹 페이지를 만드려고 한다.
- 부트스트랩 사이트에서 마음에 드는 템플릿을 다운 받는다

<p align="center"><img src="/images/AWS/AWSGuide/S3_시작하기/S3Start9.jpg"></p>

- 다운받은 템플릿의 압축을 풀면 다음과 같은 파일들이 생겨난다.

---

<p align="center"><img src="/images/AWS/AWSGuide/S3_시작하기/S3Start10.jpg"></p>

- 해당 파일 전부를 업로드를 한다.

<p align="center"><img src="/images/AWS/AWSGuide/S3_시작하기/S3Start11.jpg"></p>

- 퍼블릭 권한 관리에서 "이 객체를 퍼블릭 읽기 엑세스 권한을 부여함"을 선택한다.

<p align="center"><img src="/images/AWS/AWSGuide/S3_시작하기/S3Start12.jpg"></p>

- 스토리지 클래스는 기본인 스탠다드를 선택한다.

---

<p align="center"><img src="/images/AWS/AWSGuide/S3_시작하기/S3Start13.jpg"></p>

- 완료 후 속성의 정적 웹 사이트 호스팅을 선택한다.

<p align="center"><img src="/images/AWS/AWSGuide/S3_시작하기/S3Start14.jpg"></p>

- 이 버킷을 사용하여 웹 사이트를 호스팅합니다를 선탣한다.
- 인덱스 문서는 엔드 포인트로 index.html을 입력한다.

<p align="center"><img src="/images/AWS/AWSGuide/S3_시작하기/S3Start15.jpg"></p>

- 엔드포인트는 다음과 같다.

---

<p align="center"><img src="/images/AWS/AWSGuide/S3_시작하기/S3Start16.jpg"></p>

- 해당 엔드 포인트를 웹 브라우저에 입력하면 해당하는 웹 페이지가 정상적으로 뜨는 것을 볼 수 있다.

---
