---
title: "[javascript] 변수선언, 호이스팅, typeof, 삼항 조건 연산자"
tags:
- javascript
categories:
- javascript
date: '2021-09-14 04:26:57 +0900'
classes: wide
last_modified_at: '2021-09-14 06:38:01 +0900'
---
## 데이터타입 종류
- number(숫자)
- String(문자)
- boolean(참,거짓) : false-> 0, '', NaN, undifined
- null : 값이 텅텅 빈 변수
- undifined : 값이 텅텅 비었는지, 값을 넣을건지 아직 정해지지 않은 변수 
  - let a; 같이 값이 할당되지 않는거
- object
- fucntion  
- symbol : 고유한 식별자를 만들때 사용

```javascript
const symbol1 = Symbol('id1');
const symbol2 = Symbol('id1');
consol.log(symbol1 === symbol2); // false
//식별자는 같지만, 다른 symbol


const symbol3 = Symbol.for('id1');
const symbol4 = Symbol.for('id1');
consol.log(symbol3 === symbol4); // true
//같은 이름의 식별자를 동일하게 사용할려면 for 메소드 사용
```
<br>
<br>

- 자바스크립트는 동적 데이터타입 할당이여서, String 변수에 nubmer를 넣을수도 있고 반대로 Nubmer 변수에 String 값 할당가능. 자동으로 형변환이됨.

```javascript
let a = 'test';
a = 7;
a = '7'+5; // 75
a = '10' / '5' // 2
```

<br>
<br>

## 변수선언

var
- 재생성 가능, 값도 변경가능, 
- 변수 선언전에 값 변경, 값출력 가능 (undifined 로 표시됨. 호이스팅)
- 블록스코프 무시함 { } 안에 선언했는데 밖에서도 값을 접근하고 쓸수있음.
- 웬만하면 var 사용은 피해서 사용하는게 좋음.

<br>

let
- 재생성 불가, 값은 변경가능
- 변수 선언전에 값 변경, 출력 불가
- mutable 데이터 타입 (변경 가능)

<br>

const
- 재생성 불가, 값도 변경불가
- immutable 데이터 타입 (변경 불가)
- security
- thread safety
- reduce human mistakes 등의 이유로 사용

<br>

"" 문자열 큰따움표 안에 태그 입력시 태그 자동적용

<br>

ex)

```javascript
var tag = "<h1> String </h1>";

var s; // ---> undifined
//undifined : 값이 등록되기 전의 값

if(undifined){ //---> false 반환

};


//null : 변수에 저장된 값이 null. 대체로 저장된 값을 비울때 사용
var t = hello;
t = null;

const infinity = 1 / 0; //무한대의 값이 나오면 Infinity 자료형이 됨
const nagativeInfinty = -1 / 0 //-무한대의 값이 나오면 -Infinity 자료형이 됨
const nAn = '홍길동' / 2; // nan , Not a number 즉 숫자가 아닌 자료형이 됨

const bigInt = 123456789n; // 최근에 추가된 데이터타입. 숫자 끝에 n 을 붙이면됨

let testString = "naver";

const fstring = "${naver} 의 주소는 naver.com 이다."
// template literals
// 파이썬의 fstring 과 비슷한기능. ${변수} 하면 변수의 문자열값이 대입되어 출력됨


```

<br>

## 호이스팅
- 어디에 변수를 선언했는지에 관계없이 항상 맨위로 선언을 끌어 올려주는 기능

<br>

## First-class function
- 변수에 함수를 할당가능
- 함수의 매개변수로 함수를 넣는것도 가능
- 함수의 리턴타입을 함수로 하는것도 가능.
- 데이터 타입 변수, 자료형이 할수있는건 다 가능하다고 보면됨.

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