---
title: "[javascript] 출력, 주석, async & defer"
tags:
- javascript
categories:
- javascript
date: '2021-09-14 04:10:57'
classes: wide
---

## 출력
document.writ("메세지");

<br>

## 주석
// 한줄

<br>

/* <br>
여러줄 <br>
*/

<br>

## 외부의 자바스크립트 파일 HTML로 불러오기
- 스크립트 src = JS파일 주소

test.html 파일

```html
<head>
<script src = JS파일 경로></script>
</head>
```

<br>

example.js 파일
```javascirpt
document.write("hello world");
```

<br>

- head 에 javascript 넣을시에 브라우저가 HTML을 파싱하다가 도중에 서버에서 JS 파일을 받아오기까지 시간의 텀이 생김

- JS 파일이 클수록 HTML 전체로딩의 시간의 텀도 커짐

<br>

---> parsing HTML ---> (block) ---> fetching JS ---> executing JS ---> parsing HTML

<br>

```html
<body>
    <div>코드</div>
    <script src = JS파일 경로></script>
</body>
```

- body 에 javascript 넣을시에 홈페이지가 js에 너무 의존적인 구조라면 역시 전체적인 HTML 보기까지의 시간이 오래걸림

<br>
<br>

## head + async
```html
<head>
    <script asyn src =JS파일 경로></script>
</head>
```

- async 는 boolean 타입
- 브라우저가 HTML 을 파싱하다가 scirpt 구문 만나면 JS파일을 병렬로 다운로드 진행하고, JS파일을 다운로드 완료하면 HTML파싱을 잠시 멈추고 JS파일을 실행하는 방법

- JS파일 다운로드 체감은 늦출수 있지만, HTML파싱 도중에 JS파일을 실행해서, 조작하려는 요소등이 정의되어있지 않아서 문제가 생길수 있음

- HTML 파싱하는 도중에 여전히 멈추는 구간이 (JS 실행구간) 존재해서, HTML 로딩까지의 시간이 있음

- 다수의 JS파일1, JS파일2, JS파일3 ... 다운시에 먼저 다운로드 된 JS파일을 실행해서 JS파일 실행순서에 의존적인 홈페이지라면 문제발생

<br>

## Head + defer
```html
<head>
    <script defer src = JS파일 경로></script>
</head>
```

- HTML을 파싱 하는 도중에 Script 구문 만나면 병렬로 JS 파일다운
- HTML파싱은 계속 진행하고, HTML파싱이 다 끝난 다음에야 JS 파일 실행

- 다수의 JS파일 다운로드 시에 html파일에 정의한 순서대로 JS파일 실행함

ex) html파싱 ---> JS파일다운, HTML파싱 ---> HTML파싱 진행중, JS파일다운 완료 ----> HTML 파싱 ---> HTML 파싱완료 ---> JS 파일 실행

<br>
<br>

## use strict
```javascript
a = 6; // 에러. 선언되지 않았는데 값 할당. 하지만 동작시에는 에러가 안뜸

`use strict`;
//ECMA Script 5에 추가됨.
//문법 오류, 구문 오류 등 사전에 에러표시 해줌.
//javascript 첫구문에 쓰면좋음
```