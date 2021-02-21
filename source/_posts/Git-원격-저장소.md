---
title: Git 원격 저장소
date: 2021-02-21 20:34:40
tags:
    - Git
categories:
    - Git
thumbnail: /images/Git/GitStudy/gitLogo.png
---

### GIT 원격 저장소 - Remote repository
- 원격 저장소에 올리기(backup. 협업) -> 1대의 컴퓨터 안에서 원격 저장소 만드는 법, 이런 방법은 거의 활용하지도 않음


#### git init --bare remote
- --bare(작업을 할 수 없고 저장소로만 사용하겠다는 옵션으로 remote라는 디렉터리 생성), working 디렉터리가 없고 .git 내용만 있음, 수정같은 작업이 불가능 함, 원격 저장소 만들때는 bare 넣는다
- git remote add origin /home/git/git/remote : origin이라는 별명으로 리모트 원격 저장소 연결함
- git remote remove origin : origin 저장소를 지운다.

- git config --global push.default matching : git이 암시적으로
- git config --global push.default simple : 새 버전부터 simple 방식으로 push 하는 것이 좋음 -> 이에 대한 설정, 어디로 업로드 하겠다.
- git push origin master : origin 저장소에 master 브랜치를 저장한다
- git push --set-upstream origin master : 앞으로 push는 origin에 master를 하겠다


---------------------------------------

### Github
- 원격저장소는 구축하기 어렵기 때문에 제공해주는 서비스를 이용
- 그 중 대표적인 예가 Github -> 오픈소스 프로젝트들의 작업장
- 이미 존재하는 오픈소스 가져오기
- git/git : git에 대한 오픈소스 코드

---------------------------------------

- commits : 지금까지 commit 횟수
- branches : branch의 개수
- contributes : 이 소스코드에 접근할 수 있는 사람들
- watch : 지켜보는 사람들
- star : 좋아요 수
- fork : 해당 소스 코드를 내것으로 해서 수정이 가능(ghdrlgus96/git 이 된다) -> fork의 수가 그 소스코드의 수준을 보여준다.

---------------------------------------

- git clone https://github.com/git/git.git gitsrc : gitsrc 이름으로 clone
- git log --reverse : log를 거꾸로 봄 -> 첫번째 로그를 볼 수 있음
- git checkout (해당 commit) : 해당 commit일때 상태로 이동

---------------------------------------

### 원격 저장소 만들기
1. new repository
2. git init
3. git add .
4. git commit -m "1"
5. git remote add origin https://github.com/ghdrlgus96/git.git : 원격 저장소(remote repository)를 연결 시키고 origin 이라는 별명을 부여하겠다.

- git remote : 원격저장소 확인
- git remote -v : 상세 보기
- 작업한 내용을 여러 저장소를 remote로 해서 보낼 수 있다.
- git remote remove friend : friend remote 삭제
- git push origin master : 현재 checkout 되어있는 브랜치를 origin의 master 브랜치를 서로 연결시킨다.
- git clone https://github.com/ghdrlgus96/git.git .
- git commit --amend : 최근 커밋의 메시지 변경

##### push 이후의 내용은 수정하지 말자
- git push origin master

- //다른 로컬 저장소
- git pull origin master : 가져오기(공재 저장소에서 가져오므로 비밀번호를 묻지 않음)

- git add .
- git commit -m "2"
- git push

- //다른 로컬 저장소
- git pull ...

---------------------------------------

### 지역 저장소에서 원격 저장소를 만들어 올리기
1. git init local
2. cd local
3. git commit -am "1"

- 원격 저장소
4. git init --bare remote
5. cd remote

- 로컬 저장소
6. git remote add origin ssh://git@13.124.42.13/home/7. git/git/remote/ : ssh로 접속하는데 사용자 이름은 8. git
9. git remote -v
10. git push --set-upstream origin master

- 원격 저장소
11. git log

#### 백업 및 동기화의 의미를 갖는다.
- git clone ssh://git@13.124.42.13/home/git/git/remote/ office

---------------------------------------

### push pull
- push 전에 로컬과 원격 저장소의 내용이 다르면 pull을 하고 push를 하라
- 분산관리 시스템 특징 : 로컬에서 버전관리 하다가 필요시 원격과 동기화
- 자주 pull, push를 하여 다른 사람의 push 기록을 자주 가져오도록 하자

- pull - 작업 - push
- pull, push는 자주해야 충돌 가능성을 낮춘다.

---------------------------------------

### 원격 저장소 원리
- git remote add origin git@github.com:ghdrlgus96/repo.git

#### .git/config
``` file
[remote "origin"]
   url=git@github.com:ghdrlgus96/repo.git
   fetch =+refs/heads/*:refs/remotes/origin/*
```

- git push
``` cmd
current branch master has no upstream breanch - 연결되어 있는 원격저장소 브랜치가 없다
```

- git push --set-upstream origin master : origin의 master 브랜치에 연결
- .git/config
```file
[remote "origin"]
   url=git@github.com:ghdrlgus96/repo.git
   fetch =+refs/heads/*:refs/remotes/origin/*
[branch "master"]
   remote=origin
   merge=refs/heads/master
```

#### refs/remotes/origin/master 파일
- origin으로 push한 commit이 무엇인가가 적혀있음 (원격 저장소의 master)
#### refs/heads/master
- 지역 저장소의 master내용

#### 둘이 같음 -> 인터넷에서 가져온것이 아니라, 지역에서 마지막으로 원격으로 push 했던 기록일 뿐이다.

---------------------------------------

- git log --decorate --graph

---------------------------------------

### git pull, git fetch
#### git log --decorate --all --oneline
##### pull
- 지역 저장소 master 브랜치와 원격저장소(origin)의 master의 브랜치가 같아짐
- ORIG_HEAD는 이전 commit을 가리키고 있음

##### git fetch
- 지역저장소의 master 브랜치는 6, 원격저장소 origin의 master 브랜치는 7을 가리키고 있음 -> merge되지 않음
- ORIG_HEAD가 변하지 않음
- 원격 저장소로부터 받고 병합을 안하지 때문에 원격과 지역의 차이를 비교해 볼 수 있음
- git diff HEAD origin/master : 최신 커밋과 원격의 최신을 비교 가능

- git merge origin/master : git fetch 후 병합을 해야 함
- git fetch -> git merge origin/master