---
title: Git rebase vs merge
date: 2021-02-21 20:55:43
tags:
    - Git
categories:
    - Git
thumbnail: /images/Git/GitStudy/gitLogo.png
---

### rebase vs merge
- 병합을 하지만 결과가 좀 다르다

#### merge
- master내용을 feature로 가져오고 싶다
- git checkout feature
- git merge master
- -> 공통 조상과 3way merge 실시, master는 하나 전을 가리키고 있음

#### rebase
- 공통 조장 : base
- git checkout feature
- git rebase master
- -> 임시 저장소 어딘가에 feature의 커밋들이 저장되고, feature는 master의 최신 커밋으로 checkout된다.
- -> 임시 저장소의 commit들과 f,m인 브랜치와 병합 -> 임시에 2개 커밋 있었으면 1개하고 임시에서 1개 지우고 1개 하고 임시에서 1개 지워서 새 브랜치 만듬

---------------------------------------

- merge의 경우 history가 병렬
- rebase는 history가 1개로 나아감

- 역사 파악이 더 편함
- rebase는 어렵고 위험하다
- merge는 충돌 발생해도 해결이 쉬움