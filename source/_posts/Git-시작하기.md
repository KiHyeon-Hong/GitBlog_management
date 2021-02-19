---
title: Git 시작하기
date: 2021-02-18 21:24:58
tags:
    - Git
categories:
    - Git
thumbnail: /images/Git/GitStudy/gitLogo.png
---

### Git에 대한 기초 학습 내용

#### Git
- version control system
- Backup, Recovery, Collaboration

- version control system : CVS, SVN, Git등 다양하다.
- Dropbox, Google Drive도 버전관리 시스템의 일종이다.


``` cmd
git
```
- git 입력 시 사용할 수 있는 명령어 목록이 뜬다.


---------------------------------------

#### git init
- Initialized empty Git repository in ~
- git 저장소를 초기화 한다.
- .git Directory가 생성되며 version에 관련된 정보가 저장되므로 삭제하면 안됨

##### vim
- vim f1.txt 입력시 f1.txt 파일이 생성된다.
- 입력모드와 명령모드로 구분되어 있다.(i, a, o를 통하여 입력모드로, esc를 통하여 명령모드로 전환)
- :wq를 통하여 저장 후 나가기

#### git add
- Untracked files : 디렉터리 안에는 존재하지만, 버전관리를 하기 전까지는 git이 무시한다.
-  git이 관리를 시작하기 위한 명령어가 add이다.
- git add f1.txt 후 Changes to be committed로 변경됨
- 프로젝트를 하다보면 프로젝트 핵심 파일과 임시 파일이 있는데 임시 파일은 버전 관리를 하면 안됨, 따라서 이를 배제하기 위해 관리해야 할 파일을 명확히 알려줌

---------------------------------------
#### 초기 환경 설정
- git config --global user.name KiHyeon-Hong
- git config --global user.email ghdrlgus96@gmail.com

---------------------------------------

#### git commit
- version : 모든 변화는 버전이 아니라 의미 있는 변화이다.
- 새로운 버전으로 만들기, 일정한 작업이 완결된 상태
- git commit 후 commit message를 적어야 하는데 vim이므로 vim 입력방식대로 입력을 해야 한다.

``` cmd
[master (root-commit) 4347df6] first commit
 1 file changed, 1 insertion(+)
 create mode 100644 f1.txt
```
- 수정한 후 add 명령어를 항상 적어야지 버전 관리를 시작한다.
- 새로운 파일을 버전 관리 뿐만이 아니라 버전 관리가 되고 있는 파일을 수정하더라도 add를 해야 함
- Changes not staged for commit : 수정 시 뜨는 메시지 (git status)


#### git log
- 버전 생성된 것 확인(commit history 확인)

---------------------------------------
##### git은 왜 add를 해야 하는가?
- commit 하나는 하나의 작업을 담는게 이상적이다.
- add를 통해서 commit 하고자 하는 것만 commit 할 수 있다.


##### <stage area>
- git add f1.txt를 하면 f1.txt는 stage에 올라감, commit 대기중인 파일들
- stage - repository
- commit 결과는 repository
- commit에는 각각의 고유한 id가 있음 (commit 4347df685c78fe904d0363550936367d17851481)

---------------------------------------

#### git log의 옵션들

``` cmd
git log -p
```
- 각 commit 사이의 소스 코드 차이를 보여준다.


``` cmd
git log 4347df685c78fe904d0363550936367d17851481
```
- 이 commit 이전의 commit만 보인다.


``` cmd
git diff 4347df685c78fe904d0363550936367d17851481..8d49b7cfa3e2c42d2be75e33169b640bbb48d8e9
```
- 두 commit 사이의 소스 차이를 보여준다.
- 파일 수정 후 git diff 시 : 현재 어떠한 작업이 진행되었는지 알 수 있음 -> 자기가 작업한 내용이 마지막으로 리뷰할 수 있는 기회 (git add 시 git diff로 보이지 않음, 이전 commit과의 차이를 보여줌)

---------------------------------------

#### 과거로 돌아가기
- commit을 취소하는 명령어
- 현재의 log를 취소해서 과거로 돌아가기


#### reset vs revert
- reset 시

``` cmd
git reset 8d49b7cfa3e2c42d2be75e33169b640bbb48d8e9 --hard
```
- 8d49b7cfa3e2c42d2be75e33169b640bbb48d8e9가 head로 바뀌며 이 이후의 commit이 사라짐 (--hard, --soft등 다양한 요소가 있음)
- git reset을 하더라도 실제로 삭제되지는 않고 복구가 가능
- 협업을 하게되면 원격저장소에 올라가는데 공유한 후에는 reset을 절대로 하면 안됨, 로컬에서만 reset을 써야함
- git revert : 버전을 새로 만들면서 이전 commit으로 돌아간다


---------------------------------------

- git commit --help
- git commit -a : 수정 및 삭제 파일은 자동으로 add 후 commit
- git commit -m "commit message"
- git commit -am "2" : 한번도 버전 관리, 즉 add를 하지 않은 파일을 제외하고 전부 add 후 메시지도 입력받지 않음