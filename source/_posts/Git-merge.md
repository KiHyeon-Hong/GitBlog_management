---
title: Git merge
date: 2021-02-21 20:22:41
tags:
    - Git
categories:
    - Git
thumbnail: /images/Git/GitStudy/gitLogo.png
---


### merge &  conflict
- 충돌이 발생했을 때의 처리 방법

``` cmd
CONFLICT (add/add): Merge conflict in common.txt
Auto-merging common.txt
Automatic merge failed; fix conflicts and then commit the result.
```

- index 파일에는 보통 490c7285a63e6531ea7d4b3eb3f95d0784c6066d 0 f1.txt이지만 0이 늘어난다.
- 1 -> 원본
- 2 -> 현재 브랜치의 바뀐내용
- 3 -> 병합하고 싶은 브랜치의 바뀐내용

- 자동으로 깃은 병합작업을 실시

#### MERGE_HEAD
_ MERGE_MSG : 충돌 해결 했을 때 커밋시 메시지


---------------------------------------

### 3way merge vs 2 way merge


```
ME    Base    Other    2way    3way
 A       A         x         ?         x
 B       B         B          B        B
 1       C         2          ?         ?
 x        D        D          ?        x
```
- 2way는 base를 보지 않고 2개의 차이점만을 본다
- 3way는 base를 참조해서 2개의 대상을 병합한다(훨씬 good)