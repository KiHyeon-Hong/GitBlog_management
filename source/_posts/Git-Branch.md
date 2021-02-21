---
title: Git Branch
date: 2021-02-21 19:33:38
tags:
    - Git
categories:
    - Git
thumbnail: /images/Git/GitStudy/gitLogo.png
---

### git branch
- git branch : 치면 *master라고 뜨는데 기본 브랜치를 의미한다.
- git branch exp(생성할 브랜치명) : branch를 생성한다 -> 현재 브랜치 상태를 그대로 복사한다.
- 현재 사용되는 브랜치에 *가 뜬다

### git checkout
- git checkout exp : 브랜치를 exp 브랜치로 이동
- f1.txt라는 파일이 어떤 브랜치에 있냐에 따라 내용이 완전히 달라짐 (exp branch에서 f2.txt를 만들고 add, commit하고 master branch로 넘어가면 f2.txt파일이 보이지 않음, 그러나 f2.txt파일을 만들고 add, commit을 하지 않으면 master branch로 넘어가도 사라지지 않음)

---------------------------------------

#### git log --branches --decorate --graph
- 자신이 체크아웃된 브랜치 말고 모든 브랜치를 보여줌
- HEAD -> exp 되면 현재의 브랜치
- --graph 하면 흐름을 알 수 있음

#### git log --branches --decorate --graph --oneline
- 1줄로 현재의 상태를 보여줌

---------------------------------------

- git log master..exp : 2개의 브랜치 사이의 차이를 보여줌
- git log exp..master : exp에는 없고 master에는 있는 것들

- git log -p exp..master : 소스코드의 차이까지 보여줌

- git diff master..exp : master와 exp의 현재 상태를 비교 함

---------------------------------------

### Branch 병합

#### exp에서 작업했던 내용을 master로 병합을 하고 싶다 (그 반대와는 다름)
- exp => master로 병합을 원할 경우 master에 checkout을 한 후 master에서 merge 명령어를 작성
- git merge exp : master에서 실행하면 exp를 master로 병합
- merge된 commit은 2개의 부모를 갖는다 (exp와 master였던 것)
- git checkout exp -> git merge master
- git branch -d exp : exp branch를 삭제한다

#### 병합 순서
- git checkout -b test = git branch test -> git checkout test


#### merge를 했을 때 Fast-forward가 뜰 경우
- branch 후 아무 일도 하지 않고 merge를 할 경우 이동만 시키면 병합 작업이 끝남 fast-forword하면 별도의 commit을 생성하지 않음, 바꾸기만 함

#### merge made by the 'recursive' strategy가 뜰 경우
- fast-forward를 할 수 없는 경우이다 두 commit의 공통의 조상을 찾고, 두 commit을 합치고 합친 것을 알려주고, 합친 새로운 commit을 자동으로 생성한다.
- fast-forard가 아닌 방식은 merge commit을 생성한다.

---------------------------------------

### Stash
- branch에서 작업하다가 다른 branch로 checkout해야 하는 경우, commit하기도 애매하고 commit하지 않으면 checkout을 할수 없을 경우에 사용
- 작업한 내용을 숨겨놓고 그 브랜치의 최신 commit(head)의 버전으로 이동해서 깔끔하게 하고 다른 브랜치로 checkout 할 수 있음

- exp 브랜치에서 작업하였지만, add, commit을 하지 않으면 master로 checkout을 했을때 add되지 않았다고 뜸 -> exp에서 한 작업이 master에게 까지 영향을 미침

#### git stash
- Saved working directory and index state WIP on exp: b416d47 Merge branch 'exp', 워킹 디렉터리의 내용이 저장되었고 인덱스 내용도 세이브되었음 exp에
- exp, master에서 git status하면 작업했던 내용들이 숨겨져서 사라짐

- git stash apply : 숨겨진 파일을 다시 불러옴
- git stash list : list를 볼 수 있음

---------------------------------------

#### git reset --hard HEAD
- 가장 최신 커밋 상태로 우리의 워킹 카피를 보냄, stash의 내용은 사라지지 않음! -> 명시적으로 삭제를 하지 않는한 살아있음
- git stash apply를 통하여 다시 숨겨놓은 것을 받아올 수 있음 (가장 최근의 stash를 적용함)
- git stash drop : 가장 최근의 stash를 삭제
- stash를 전부 적용하기 위해 apply -> drop -> apply -> drop을 반복한다

- git stash pop : apply drop까지 됨
- stash는 워킹 디렉터리의 변경사항을 감추는 것이다
- add 하지 않은 것은 stash를 하더라도 숨겨지지 않는다 (untracked) -> stash는 최소한 버전관리중인 파일에 대해서만 적용이 된다.

---------------------------------------

### Branch 상세
- .git의 HEAD 파일 -> refs/heads/master : objects의 id, 즉 commit의 object id를 가리키고 있음
- 새로운 commit 시 방금 commit으로 바뀜(가장 최신의 commits), 그리고 해당 commit의 parent를 통해서 탐색해 갈 수 있음

#### 새로운 branch 생성
- refs/heads/exp가 생성되며 최신 commits을 가리킨다
- rm .git/refs/heads/exp를 하면 삭제 가능
- git에서 브랜치는 매우 중요하지만 단순한 파일일 뿐이다
- HEAD는 head를 가리킴 git checkout 시 HEAD 내용이 바뀜

---------------------------------------

### Branch 병합 과정의 충돌
- merge 과정에서 파일의 내용이 다를 경우
- 같은 파일임에도 서로 수정하는 위치가 다르다면 자동으로 합쳐준다
- ex}
1. master -> function a(기존), function b(추가)
2. exp -> function c(추가), function a(기존)
3. merge -> function c, finction a, function b

#### but, 수정하는 위치가 같다면
- ex) function a(master){}, function a(exp){}

``` cmd
CONFLICT (add/add): Merge conflict in common.txt
Auto-merging common.txt
Automatic merge failed; fix conflicts and then commit the result.
```

#### git status 시
``` cmd
Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both added:      common.txt
```

---------------------------------------

### vi common.txt 시

```
- ======= 구분자 중심으로
- <<<<<<< HEAD : 현재 checkout branch
- >>>>>>> exp : exp branch의 내용
```

- 자기가 자동 merge 실패하였기 때문에 충돌을 해결하라
- 충돌이 난 부분 표시이다 -> 문제를 수정하자
- 그 후 git add common.txt
- git commit (보면 충돌난 것 해결했다고 메시지가 뜸)

#### git add 없이 merge를 또 시도할 경우 뜨는 에러

``` cmd
error: Merging is not possible because you have unmerged files.
hint: Fix them up in the work tree, and then use 'git add/rm <file>'
hint: as appropriate to mark resolution and make a commit.
fatal: Exiting because of an unresolved conflict.
```