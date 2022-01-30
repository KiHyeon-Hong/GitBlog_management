---
title: Git 저장소 원리
date: 2021-02-21 20:20:31
tags:
  - Git
categories:
  - Git
thumbnail: /images/Git/GitStudy/gitLogo.png
---

## working copy & index & repository

- working directory(working tree, working copy), index(git add 시, staging area, chche), repository(commit이 저장, history, tree)
- git reset --hard하면 저장소, add, working까지 삭제됨
- git reset --soft하면 repository만 삭제됨
- git reset --mixed하면 레포지토리랑 add 삭제됨

- git reset --soft 490c7285a63e6531ea7d4b3eb3f95d0784c6066d
- git diff : working copy와 index 비교
- git reset --hard : 최신 커밋 상태로 바꿔버림 working copy까지
