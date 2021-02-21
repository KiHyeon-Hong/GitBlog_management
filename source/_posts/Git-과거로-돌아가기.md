---
title: Git 과거로 돌아가기
date: 2021-02-21 20:15:04
tags:
    - Git
categories:
    - Git
thumbnail: /images/Git/GitStudy/gitLogo.png
---

### Reset checkout
- 과거로 돌아가고 그 뒤에 있는 commit을 삭제하고 싶다.
- git reset --hard 490c7285a63e6531ea7d4b3eb3f95d0784c6066d
- HEAD인 refs/heads/master가 490c7285a63e6531ea7d4b3eb3f95d0784c6066d을 가리키게 된다.
- 그러나 정보는 최대한 지우지 않는다

#### reest 취소 방법
- ORIG_HEAD 파일은 reset 전 head가 있다(현재 branch의 최신 commit, 즉 head가 가리키는 것을 저장)
- logs/refs/heads/master는 head 기록이 남는다 - 기록 역사(head 변경의 역사)
- git log --hard ORIG_HEAD : 기존의 head로 다시 돌아옴
- git reflog : 각각의 commit들이 기록됨


#### checkout으로 돌아가는 법
- checkout 뒤에다가 commit id를 직접 적을 수 있다
- git checkout 490c7285a63e6531ea7d4b3eb3f95d0784c6066d

```
You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.
```

---------------------------------------

#### $ git branch
- * (HEAD detached at 490c728)
- HEAD 파일을 보면 직접 commit id를 가리킴
- 다시 git checkout master를 통하여 돌아오면 됨