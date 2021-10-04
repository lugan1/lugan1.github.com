---
title: "[javascript] 변수, 데이터타입, 호이스팅, typeof, 조건 연산자"
tags:
- javascript
categories:
- javascript
date: '2021-09-14 04:26:57'
classes: wide
last_modified_at: '2021-09-14 06:38:01 +0900'
---
## 데이터타입 종류

### 기본타입
- number(숫자)
  - 자바스크립트는 하나의 숫자형만 존재함
  - 모든 숫자를 64비트 부동소수점 형태로 저장하기 때문이다.
  - 5 / 2 같은 연산은 정수로 처리하는 것이 아닌 **실수로 처리되어서 실수값 2.5가 나온다.**
- String(문자)
  - 자바스크립트에서는 한번 생성된 문자열은 읽기만 가능하고 수정은 불가능하다.
  - a = "asdf" ; a = "qwer"; 값이 변경된거 같지만 a를 새로 만든거임

- boolean(참,거짓) : false-> 0, '', NaN, undifined
- null : 값이 텅텅 빈 변수. 
  - 개발자가 명시적으로 값이 비어있음을 나타내는데 사용.
  - null 타입 변수를 typeof 연산자로 검사하면 object로 뜸
  - 따라서 a === null 과 같이 typeof 쓰지말고 그냥 ===연산자로 null 검사해야됨.

- undifined : 값이 텅텅 비었는지, 값을 넣을건지 아직 정해지지 않은 변수
  - let a; 같이 값이 할당되지 않는거

### 참조타입  
- object
  - Array
  - Fucntion
  - Regexp (정규표현식)
  - symbol : 고유한 식별자를 만들때 사용

```javascript
//자바스크립트의 문자열은 불변임, 값 변경 불가
var str = 'test';

str[0] = 'W';
console.log(str) // 출력값 test

var a = "asdf";
a = "qwer";
//값이 변경된거 같지만 a를 새로 만든거임
//str[1] = "ㄹ" 이런식으로 인덱스 연산자를 이용한 값변경은 안됨




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

const fstring = "${testString} 의 주소는 naver.com 이다."
// template literals
// 파이썬의 fstring 과 비슷한기능. ${변수} 하면 변수의 문자열값이 대입되어 출력됨


```

<br>

## 호이스팅
- 어디에 변수를 선언했는지에 관계없이 항상 맨위로 선언을 끌어 올려주는 기능

<br>

## First-class function (함수 표현식)
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