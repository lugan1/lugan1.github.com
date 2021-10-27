---
title: "[git] 소스트리 git 사용법 정리 "
tags:
- git
- 소스트리
categories:
- git
date: '2021-10-22 09:00:00'
classes: wide
---

# git add / commit / push
- 소스트리에서는 파일 내용이 변경시 바로바로 감지되어 커밋하지 않은 변경사항이라고 표시된다. 

<br/>

# git add
- 소스트리에서 모두 스테이지에 올리기 / 선택내용 스테이지에 올리기는 git add 파일 명령어와 동일하다.

- 스테이지에 올라가지 않을 파일 리스트 옆에 (+)를 눌러도 동일하게 git add 가 적용되어 스테이지에 올라간다.

- commit 을 위한 후보를 선택하는 것으로 보면된다. 아직까지 commit 은 안되었고 후보를 선택했다.

# git commit
- 스테이지에 올라간 파일들은 소스트리 하단의 텍스트창에서 commit 메세지를 작성할수 있다. 

- \[커밋] 버튼을 누르면 git commit -m (메세지) 와 동일하게 커밋된다.

- commit을 완료하면 소스트리 좌측 사이드바의 History 메뉴에서 추가된 커밋 크래프를 확인할 수 있다.

## origin / master
- 소스트리 History 에서 보면 origin과 master , 혹은 origin/master 라는 꼬리표가 붙은것을 확인할수 있는데 의미는 다음과 같다.

- 소스트리의 history 그래프의 origin / master를 요약하면 아무것도 붙지않은 \[master]는 내 컴퓨터 로컬 저장소 버전을 나타내고, \[origin/master]는 github의 원격저장소 버전을 가리킨다.

### origin
- 현재 프로젝트의 파일들과 원격으로 연결되있는 github 원격저장소의 닉네임
- 따로 원격저장소 네임을 설정 안했으면 디폴트로 origin 으로 설정되는듯하다.
- 요약하면 원격저장소의 현재 버전 상태를 가리키는 커밋에 origin 이라는 꼬리표가 붙어있다.

### master
- 우리가 커밋을 올리는 브랜치의 이름
- 따로 브랜치를 생성하지 않으면 git은 master라는 기본 줄기에 커밋을 한다.

<br/>

# git push
- 소스트리 상단 메뉴에서 push를 누르면 push 설정창이 뜬다.
- push 설정창에서 각 브랜치들을 체크박스로 설정할 수 있다.
- 체크박스를 설정하고 push를 진행하면 체크박스를 선택한 브랜치들에게 push가 진행된다.
- 만약 master 브랜치를 선택하고 push를 했으면 git -push origin master와 동일하다.
