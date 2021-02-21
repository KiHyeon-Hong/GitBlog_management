---
title: Git 원리
date: 2021-02-19 22:17:49
tags:
    - Git
categories:
    - Git
thumbnail: /images/Git/GitStudy/gitLogo.png
---

### .git directory
- git add 시 : index, objects directory가 변경됨
- objects directory 내부에는 git add한 기록이 있으며, 이에 대한 자세한 내용은 index에 존재함
index : 100644 8d49b7cfa3e2c42d2be75e33169b640bbb48d8e9 0 f1.txt

#### cp 명령어로 파일을 복사할 경우
- cp 명령어를 쓰면 같은 8d49b7cfa3e2c42d2be75e33169b640bbb48d8e9를 갖는다 -> 같은 object를 갖는다
- 파일의 이름이 달라도 내용이 같으면 같은 object를 갖는다
- 내용이 a라면 같은 8d49b7cfa3e2c42d2be75e33169b640bbb48d8e9를 가질 것이다 (이 세상 누가 작성하더라도)

#### objects 파일명과 원리
SHA1 online -> hash, 일정한 길이, git은 SHA1을 통과시켜서 hash값에서 2글자 빼고 objects 디렉터리를 만들고 그 나머지를 파일을 만들어서 정보를 저장한다.
- git add를 하면 git은 add한 파일의 내용과 부가적인 정보로 hash를 통과시키고 디렉터리와 파일을 만들고 그 정보를 저장한다음 index파일에서 이를 표시해준다.

#### commit의 원리
- git commit -m "1" 시
- objects 디렉터리 안에 commit 정보가 저장, commit도 내부적으로는 객체
- tree 8d49b7cfa3e2c42d2be75e33169b640bbb48d8e9 -> 트리는 해당 버전의 파일의 이름과 그 내용 해쉬가 있음
- parent에는 이전 commit을 볼 수 있음
- 각각의 버전은 그 버전이 만들었을 때의 스냅샷을 찍는다
- objects 파일의 3가지 : 파일의 내용blob, 디렉터리 파일명과 파일명의 blob에 대한 정보tree, commit

---------------------------------------

#### git status의 원리
- index 파일은 무엇일까
index와 최신 objects에 있는 commit을 비교 -> 일치한다면 commit할 내용이 없음
- index의 hash와 실제 디렉터리 hash가 다르면 수정되었음을 알림

- add 하면 objects에 새로운 것이 생성되었고 index에 반영됨, 실제 파일과 hash는 같음, 그러나 가장 최신 커밋이 가리키는 f2.txt의 hash와는 다르므로 현재 f2.txt는 add되고 commit 대기 상태임을 알 수 있음
- 프로젝트 폴더(working directory, work tree), index, objects, 최신 commit이 전부 일치하면 commit할 것이 없다고 알려줌

---------------------------------------

working directory, work tree - index, staging area, cache - repository