---
title: "[javascript] 객체, 배열, 문자열"
tags:
- javascript
categories:
- javascript
date: '2021-09-14 04:28:57 +0900'
classes: wide
last_modified_at: '2021-09-14 14:57:01 +0900'
---

## 브라우저 객체모델 (BOM) 메소드들 맛보기
prmpot() 메소드
- 프롬프트 창 출력
- prompt("텍스트", 디폴트값);
- ex) var a = prompt("A의 값 입력", 0);

confirm() 메소드
- 다이얼로그 창 출력
- confirm("메세지");
- ex) var result = confirm("확인누를시 true, 취소 누를시 false 반환");

alert() 메소드
- 얼럿 창 출력 (확인 버튼밖에 없음)
- alert("메세지");

location.reload() 메소드
- 브라우저 새로고침

location.href = "주소"
- 해당 하이퍼링크 주소로 자동이동.

console.log(문자열) 메소드
- 브라우저에서 F12 누르고, Console 탭 누르면 해당 로그 찍힘

<br>
<br>

## 객체
- 자바스크립트는 객체기반 언어
- 객체.메서드(); 등 , 기본 객체 활용법은 자바랑 같음

<br>

객체의 종류
1. 내장객체 : 문자, 날짜, 배열, 수학 등 유용한 기본 내장객체
2. 브라우저 객체 모델(BOM) : 
window, screen, location, history, navigator등, 브라우저에 계층구조로 내장되어있는 객체
3. 문서 객체 모델(DOM) :
 - HTML 문서구조 \<html>,\<head>,\<body> 등 HTML 태그 관련
 - IE 8 이하 버전에서는 호환성이 떨어지기 때문에 제이쿼리 문서 객체 모델을 많이사용

 <br>

 객체 생성하기
- 자바는 (자료클래스형) (이름) = new (자료클래스형) 인데, 자바스크립트는 자료클래스형 대신 var 로 땡칠수있음.
- ex) var 인스턴스 = new 자료클래스형();
- 자바처럼 클래스 생성후, 생성자 등 안만들어도됨. 먼저 생성후 변수값 설정가능
- 생성자도 설정시 생성자 만들수있음
- 자바처럼 this 키워드 사용
- 메소드 생성시에는 function() { 처리내용 } 으로 메소드 구현

```javascript
//먼저 객체 생성후 변수 및 메소드 설정
var tv = new Object();
tv.color = "white";
tv.info = function(){
 document.write("tv 색상 :"+this.color);
{

//객체 선언 후, 메소드 호출 (대입이 아니라 선언이라 =대신 : 사용)
var car = {
 color : "black"
 info: function(){
 document.wirte("tv 색상 :"+this.color);
 }
};

tv.info();
car.info();
```

<br>

## 배열 객체
- 한 배열에 숫자형, 문자형, boolean 형 값들을 같이 넣을수 있음
<br>var 참조변수 = new Array();
<br>var 참조변수 = new Array(값1, 값2, 값3);
<br>var 참조변수 = [값1, 값2, 값3];

- ex) var testArray = new Array(30, "따르릉", true);

<br>배열 중요 메서드

- splice() -> 지정 데이터를 삭제하고, 그 구간에 새 데이터 삽입
- pop() -> 배열 마지막 인덱스의 데이터를 가져옴 (빼옴)
- shift() -> 배열 첫번째 인덱스의 데이터를 가져옴 (빼옴)
- push() -> 배열 마지막에 데이터를 밀어넣음
- unshift() -> 배열 첫번째에 데이터를 밀어넣음

```javascript
var greenArr = ["교대", "방배", "강남"];
//교대(0), 방배(1), 강남(2)

var yellowArrr = ["미금", "정자", "수서"];
//미금(0), 정자(1), 수서(2)

greenArr.splice(2, 1, "서초", "역삼");
// 2번째 인덱스부터 1개의 데이터 삭제후, 서초 역삼 삽입

console.log(greenArr);
// ["교대", "방배", "서초", "역삼"]

var 수서 = yellowArr.pop();
var 미금 = yellowArr.shift();

yellowArr.push(미금);
console.log(yellowArr);
// ["정자", "미금"]

yellowArr.unshift(수서);
console.log(yellowArr);
// ["수서", "정자", "미금"]
```

<br>
<br>

## 문자열 객체
```javascript
var 참조변수 = new String(문자형 데이터);
//혹은
var 참조변수 = 문자형데이터
//으로 문자열 객체 선언
```

- indexOf() 메소드 : 해당하는 문자의 index 반환, 파이썬의 in 과 같은형식으로 문자열에 해당문자가 포함되는지 확인할수 있음

```javascript
var testString = "you lucky guy";
var check1 = false;

if (testString.indexOf("lucky") > 0 ){
    console.log("true");
}
// indexOf(문자열) > 0 형식으로 문자가 포함되어있는지 확인할수 있음
```

