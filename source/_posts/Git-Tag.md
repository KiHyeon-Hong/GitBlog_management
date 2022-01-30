---
title: Git Tag
date: 2021-02-21 20:50:03
tags:
  - Git
categories:
  - Git
thumbnail: /images/Git/GitStudy/gitLogo.png
---

## Tag

- 태그는 언제나 똑같은 것을 가리켜야 한다
- 현재 버전의 상태를 다운로드 하고 싶다

### git tag 1.0.0

- 현재 master 브랜치에서 태그가 만들어진다
- git tag master
- git tag (커밋번호)

- 브랜치와는 달리 태그는 항상 일정한 것을 가리킨다
- git checkout 1.0.0(태그명) : 테그명을 입력하면 해당 커밋으로 넘어갈 수 있다.

---

### Annotated Tag

- 태그에 대해 좀 더 자세한 설명을 추가하고 싶을 때
- git tag -a 1.1.0 -m "bug fix" master : 어노테이션 태그
- git tag -v 1.1.0 : 상세한 태그 설명을 볼 수 있음

### 태그를 올리고 싶으면

- git push --tags origin master : --tags가 없으면 태그는 원격 저장소로 가지 않음
- 올라갈 태그는 releases로 올라감
- git tag -d 1.1.0 : 태그 삭제

---

## Tag의 원리

- git tag 1.1.2
- refs/tags/1.1.2 : 텍스트 파일이고 내용은 objets id 가리키며, commit을 가리킨다.

- git tag -a 1.1.3 -m "bug fix"

### objects/3e/...

- 특정한 오비젝트 가리키며 커밋을 가리킴
- 태그 이름과 태그 내용 또한 저장됨
- refs/tags/1.1.3 : 3e...인 objects밑의 태그를 가리킴
