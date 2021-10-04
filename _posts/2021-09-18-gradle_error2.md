---
title: "[spring] Could not find method compile() for arguments 오류 해결법"
tags:
- error
- java
categories:
- spring
date: '2021-09-18 03:31:57'
classes: wide
---

## Could not find method compile() for arguments 오류 해결법
- CMD 에서 gradle wrapper 명령어 사용시 나오는 오류
- gradle version 7.2 에서 build.gradle 에서 compile 명령어 쓰면 나옴

- compile -> implementation 으로 수정하면 해결

