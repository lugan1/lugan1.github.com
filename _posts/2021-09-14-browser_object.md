---
title: "[javascript] 브라우저 객체 모델(BOM)"
tags:
- javascript
categories:
- javascript
date: '2021-09-14 15:00:57 +0900'
classes: wide
last_modified_at: '2021-09-14 22:46:01 +0900'
---

## 브라우저 객체 모델 (BOM)
- 브라우저에 내장된 객체
- window 는 브라우저 객체의 최상위 객체
- 계층적 구조로 이루어져 있음

<br>
<br>

window 객체의 하위 객체들
- documunt
- screen
- location
- history
- navigator

<br>

window 객체의 메서드

|종류|설명|
|---|---|
|open("URL", "새창이름", "새창옵션")| URL페이지를 새창으로 띄움 (팝업)|
|alert("문자열")|경고창을 띄움|
|prompot("문자열", "디폴트값")| 프롬프트 창을 띄움|
|confirm("문자열")| confirm 창 띄움. 확인 버튼 누를시 true 반환, 취소버튼 누를시 false 반환|
|moveTo(x, y)| 지정한 위치로 창 이동|
|resizeTo(width, height)|지정한 크기로 창 크기 변경|
|setInterval( fucntion(){ 처리내용 }, 3000) | 일정 간격으로 함수호출해서 코드실행. 예시는 3초 마다 실행|
|setTimeout( function(){ 처리내용 }, 3000) | 일정 시간 후에 함수 호출해서 코드실행. 예시는 3초후에 실행|


- clearInterval(인터벌함수), clearTimeout(setTime함수) 는 각각 해당되는 함수 정지 및 제거

<br>
<br>

open() 메소드의 새 창 옵션 종류
- open()메소드 매개변수에 url 대신 HTML파일 주소를 넣으면 html파일 띄움

|속성|설명|
|---|---|
|width|너비 설정|
|height|높이 설정|
|left|수평 (x축) 위치 설정|
|top|수직 (y축) 위치 설정|
|scrollbars|스크롤바의 숨김/노출 설정. = yes 노출/ = no 숨김|
|location|URL주소 입력 영역 숨김/노출 설정. = yes 노출/ = no 숨김|
|status|상태 표시줄 영역 숨김/노출 설정. = yes 노출/ = no 숨김|
|toolbars|도구 상자 영역의 숨김/노출 설정. = yes 노출/ = no 숨김|

<br>
<br>


## 일정한 시간 간격으로 코드 실행하기
- setInterval(함수 구현, 시간) : 일정한 간격으로 함수 실행
- clearInterval(멈출 함수) : setInterval 작동 취소

<br>
<br>

test.html
```html
<script>
val addnum = 0;
val subnum = 1000;

val auto_1 setInterval( fucntion() {
    addnum++;
    console.log("addnum: " + addnum);
}, 3000);
//3초마다 addnum 숫자 증가하고, 콘솔에 출력

val auto_2 setInterval( fucntion() {
    subnum--;
    console.log("subnum: " + subnum);
}, 3000);
//3초마다 subnum 숫자 감소하고, 콘솔에 출력
</script>



<body>
    <button onclick="clearInterval(auto_1)">증가 정지</button>

    <!-- <button onclick=처리내용> 버튼 텍스트 </button>-->

    <button onclick="clearInterval(auto_2)">감소 정지</button>
</body>
```
<br>
<br>

## document 객체
- body, div, img, a, form, input 등의 속성 정보를 가져오고, 변경 가능
```javascript
var imgTag document.getElementsById("photo");
//photo 태그의 참조 주소를 갖고옴. 리턴 타입이 photo 자료형이라고 보면됨

imgTag.setAttribute("src", "src주소 입력");
//photo 속성에서 src 값 설정 및 변경

```

<br>

## Screen 객체
- 사용자의 모니터 정보(속성) 등을 제공하는 객체
- 너비, 크기, 높이, 사용자 모니터가 표현가능 컬러bit 등 제공

<br>

## location 객체
- 사용자 브라우저의 관련된 속성과 메서드를 제공
- 새로고침, 하이퍼링크로 이동, URL의 쿼리구문 가져오기 등

<br>
<br>

## history 객체
- 페이지 이동간의 기록을 남겨 놓고, 이전방문 페이지, 다음페이지 등 페이지 이동하는 메서드 제공


<br>
<br>

## navigator 객체
- 현재 방문자가 사용하는 브라우저 정보와 운영체제 정보를 제공

<br>

navigator.~~~ 객체의 속성 종류

|종류|설명|
|---|---|
|appCodeName|현재 브라우저의 코드명을 반환|
|appName|현재 브라우저의 이름을 반환|
|appVersion|현재 브라우저의 버전 정보를 반환|
|language|현재 브라우저가 사용하고 있는 언어 반환|
|product|현재 브라우저의 엔진 이름 반환|
|platform|현재 컴퓨터의 운영체제 정보를 제공|
|online|현재 온라인 상태여부에 대한 정보를 제공|
|userAgent|운영체제의 종합 정보를 제공|
