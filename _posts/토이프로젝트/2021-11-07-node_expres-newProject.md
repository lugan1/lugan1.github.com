---
title: "[카톡봇] Node Express 프로젝트 생성"
tags:
- 토이프로젝트
- 카톡봇
- Node Express
categories:
- 토이프로젝트
date: '2021-11-07 00:33:00'
classes: wide
---

# Node Express 프로젝트 생성
## Express-Generator
- 프로젝트에 필요한 package.json 을 만들어주고 기본 폴더 구조까지 잡아주는 패키지
- 다음과 같은 명령어를 사용해 설치한다.

```
npm i -g express-generator
```

Express generator 설치가 완료 되었다면, 새 프로젝트용 폴더를 아무거나 만들고 그 프로젝트 최상위 폴더로 이동한다.  

그리고 다음과 같은 명령어를 이용해 프로젝트 초기화를 한다.

```
express <프로젝트 이름> --view-pug
```  
<br/>

프로젝트가 생성되었다면 해당 프로젝트 폴더로 이동해 다음과 같은 명령어를 실행해 npm 모듈들을 설치한다.

```
npm i
```

<br/>
<br/>

# Intellij 를 이용해 설치하는 방법
- 새 프로젝트 -> JavaScript -> Express 선택후 프로젝트 생성


# Node Express 초기 프로젝트 구조
- app.js : 핵심적인 서버역할 담당
- www : 서버를 실행하는 스크립트
- public : 외부에서 접근 가능한 파일들을 모아둔 곳
  - 이미지, 자바스크립트, CSS 파일들이 들어있다.
- routes : 주소별 라우터들을 모아둔 곳
- views : 템플릿 파일들을 모아둔 곳


서버의 로직은 routes 폴더안에 파일을 작성하고, 화면 부분은 views 폴더 안에 작성한다.

<br/>

# Express 실행방법
```
npm start
```
