---
title: "[spring] could not execute build using connection to gradle installation"
tags:
- error
- java
categories:
- srping
date: '2021-09-17 18:31:57'
classes: wide
---

스프링 프로젝트 듀토리얼을 따라하던중에 Gradle 프로젝트 생성시에 계속 'could not execute build using connection to gradle installation' 오류가 나면서 프로젝트 생성이 안되었다.


![Gradle_Error](/assets\image\posts_image\gradle_error1.png)

<br>
<br>

gradle 버전은 6.9.1 부터 6.8 까지 binary 와 complite 버전을 다시깔았다가 설치하면서 환경변수도 다시 잡고 반복을 했는데 똑같은 문구였다. 혹시나 싶어 관리자 권한으로 이클립스를 실행했는데 택도없었다. 구글링에도 답이 안나와 답도 없는 상황에서 약 2시간만에 해결되었다.

<br>
<br>

## 해결법

- Gradle 공식 홈페이지 가서 install-gradle 누르고 gradle 최신 버전을 다운받는다. (현재 시점에서는 7.2 버전이 자동 다운로드 됨)

- 환경 변수를 다시 설정한다. (내경우에는 혹시 몰라서 지역변수, 전역변수 다 설정했다. 아마 전역 변수만 설정해도 될것같다.)

- 지역변수에 변수이름 : GRADLE_HOME , 변수값 : (GRADLE폴더 경로) 를 추가한다. 튜토리얼 영상에 나와있어서 따라했다.

- 이클립스 prefrences 설정에서 gradle 설정으로 들어가서 local installation derectory 설정을 아까 다운받은 최신 gradle 압축푼 폴더 경로로 설정했다.


<br>
<br>

## 결론
아마 버전 문제인것 같다. 최신버전만 사용이 되는것 같다. 최신버전 다운받고, 최신 버전으로 환경변수 잘잡고, 이클립스 gradle 로컬 디렉터리 설정만 잘 잡으면 될것 같다.
