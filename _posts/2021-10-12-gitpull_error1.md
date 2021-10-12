---
title: "[git] git pull 에러 발생시 ( error: Your local changes to the following files would be overwritten by merge )"
classes : wide
tags:
- git
- error
categories:
- git
- error
date: '2021-10-12 08:39:00'
---

# error: Your local changes to the following files would be overwritten by merge
## 에러 원인 :
- pull 로 가져오려는 소스와, 현재 저장되어 올라가져 있지 않은 코드가 충돌이 나서 나오는 에러

## 해결 방법 : 
- git stash 명령어로 해결
- 현재 업로드 되지 않은 코드들을 임시로 다른곳에 백업하고, 깨끗한 상태로 돌려 놓는것
- 즉 현재 업로드 되지 않은 수정사항을 다른곳에 백업해서 깨끗히 만들고 git pull 로 소스를 받아와서 합치면 된다.

