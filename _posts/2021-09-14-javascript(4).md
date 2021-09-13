---
title: "[javascript] 변수선언, typeof, 삼항 조건 연산자"
tags:
- javascript
categories:
- javascript
date: '2021-09-14 04:26:57 +0900'
classes: wide
---

## 변수선언
var -> 재생성 가능, 값도 변경가능
<br>
let -> 재생성 불가, 값은 변경가능
<br>
const -> 재생성 불가, 값도 변경불가

- "" 문자열 큰따움표 안에 태그 입력시 태그 자동적용
- ex)
```javascript
var tag = "<h1> String </h1>";

var s; // ---> undifined
//undifined : 값이 등록되기 전의 값

if(undifined){ //---> false 반환

};


//null : 변수에 저장된 값이 null. 대체로 저장된 값을 비울때 사용
var t = hello;
t = null;
```

<br>

## typeof 변수
- 지정한 데이터 또는 변수의 자료형 출력

<br>

## 문자열 결합
- 문자열 결합은 자바랑 비슷함
- ex) 문자열1 + 문자열2 -> 문자열12
- ex) 문자열1 + 숫자 + 문자열2 -> 문자열1숫자문자열2

<br>


## 삼항 조건 연산자
- 조건 ? true일경우 : false일경우