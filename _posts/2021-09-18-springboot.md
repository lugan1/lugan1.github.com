---
title: "[spring] 튜토리얼(3). 스프링 부트로 헬로월드 출력하기"
tags:
- spring
- java
categories:
- spring
date: '2021-09-18 05:04:57'
classes: wide
---

이전 포스트에서 각각 메이븐 프로젝트와, 그래들 프로젝트를 생성해봤다. 프로젝트 생성부터, gradle 버전, 필요한 dependecy 설정까지 많많치 않다. dependency 를 잘못설정하면 툭하고 오류나고 빌드 자체가 안되어 버렸다.

하지만 스프링 부트를 사용하면 이러한 프로젝트 생성을 필요 dependency를 추가해서 자동으로 해준다고 한다.

<br>
<br>

## 스프링 부트
- [https://start.spring.io/](https://start.spring.io/) 에서 웹으로 실행 가능

- 스프링 관련 모듈들을 추가할때마다 dependency 문장의 길이도 길어지고 오류도 툭하면 많이 발생하고 가독성도 떨어지는데, **스프링 부트를 사용하면 dependency 문장의 길이가 확 줄어듬**

- 버전 관리도 권장 버전으로 자동 설정됨


- configration 파일도 application.properties 혹은 application.yml 파일로 쉽게 작성 가능하게됨

- 서버 설정도 간단하게 할수 있게됨. 

- 내장 서블릿 컨테이너로 jar 파일을 쉽게 배포가능

<br>
<br>
<br>

## 스프링 부트 실행방법
- 브라우저로 [https://start.spring.io/](https://start.spring.io/) 이동

- 각 메타 데이터 설정, add dependencies 버튼으로 필요 dependency 추가하고 generate 버튼 클릭


- 압축파일이 다운로드 되어지는데, 압축파일 압축풀고, IDE 이클립스나 인텔리J 로 프로젝트 열음

- 이클립스는 파일시스템 열기로 하면 안됨. import -> exisiting project into wrokspace 이걸로 열어야됨


<br>
<br>


## 스프링 부트 사용해서 Hello world 까지 띄우기
### step 1. dependency 설정에 다음과 같은 의존 추가
- Spring Web
- Spring Data JPA
- H2 Database
- Mustache

### step 2. gradle project, jar, 스프링 부트 버전은 권장버전, 자바 버전은 8 로 설정하고 Generate

<br>

### step 3. 다운받은 압축파일 풀고 IDE로 프로젝트 열기

<br>

이클립스로 프로젝트 띄울시 자바 소스파일에 **The import org.springframework cannot be resolved** 오류 해결법

- 파일 시스템 열기로 해서 생긴 오류

- file -> import -> exisiting project into wrokspace 으로 열면 해결

<br>
<br>

### step 4. 프로젝트 Run 구동 해보고, localhost\:8080 으로 페이지 이동되면 성공

### step 5. resource -> static 폴더에 hello.html 파일 생성

### step 6. \<body> 태그 안에 \<h1>hello world!\<h1> 입력

### step 7. 서버 재구동하고 localhost\:8080/hello.html 이동후 제대로 출력 되는지 확인

