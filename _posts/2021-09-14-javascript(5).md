---
title: "[javascript] 객체, 배열, 문자열"
tags:
- javascript
categories:
- javascript
date: '2021-09-14 04:28:57'
classes: wide
last_modified_at: '2021-09-16 02:27:01 +0900'
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

### 객체 생성하기
- 자바는 (자료클래스형) (이름) = new (자료클래스형) 인데, 자바스크립트는 자료클래스형 대신 var 로 땡칠수있음.
- ex) var 인스턴스 = new 자료클래스형();
- **객체 속성값 동적 추가, 동적 생성가능.**
   - 객체를 먼저 생성후에, 객체 . 필드값 으로 동적으로 필드값 추가 가능
- 생성자도 설정시 생성자 만들수있음. (fucnton 함수 형식으로 생성)
- 자바처럼 this 키워드 사용
- 메소드 생성시에는 function() { 처리내용 } 으로 메소드 구현

<br>
<br>


### 객체 생성 방법 3가지
1. new Object() 객체 생성함수 이용.
   - **객체를 먼저 생성후**, 그 객체의 필드값 추가, 설정가능.

2. 객체 리터럴 방식
   - C의 구조체랑 비슷함
   - 중괄호 var 참조변수 {   } 안에 key : value 형식으로 작성
   - value에다가 function 함수 집어넣을수 있음

3. 객체 생성자 함수 방식
   - 1.먼저 객체 생성자 함수를 만들음
   - 2.var 변수 = new 함수(매개변수); 형식으로 객체 생성

<br>
<br>

### 객체 필드값 접근 (생성)방법
1. 마침표 . 찍어서 접근
2. 객체['필드값명'] 으로 접근 (대괄호 표기법)
   - 필드값명에 연산자가 포함된경우, 대괄호 표기법으로 접근해야됨 
   - (full-name 같은경우 -연산자가 이름에 포함)
   - 만약 객체.full-name 형식으로 접근하게 되면 NaN 발생. 문자열끼리 - 연산을 하게되어서 발생되는 현상.



```javascript
//1. Object() 생성자 방식
var foo = new Object();
//객체 생성

foo.name = 'foo';
foo.age = 30;
foo.gender = 'male';
//객체를 생성후에도 그 객체의 필드값 설정가능

//2. 객체 리터럴 방식
var food{
    name : 'apple',
    price : '3000',

    printFood : function(){
        console.log(name);
    }

}

//3. 객체 생성자 함수 방식
function foo (name, price){
    this.FoodName = name;
    this.FoodPrice = price;

    this.printFood = function(){
        console.log(FoodName);
    }

 var testObject = new foo('name', 3000);
}

testObject['full-name'] = 'james lee';
//대괄호 표기법으로 객체 필드값 생성 (접근)

console.log(testObject['full-name']);

testObject.full-name = 'ABCD';
//NaN 발생. full - name (문자열끼리 - 연산을 하게됨)

```




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
<br>

## for in을 사용해 객체의 필드값들에 접근 하는방법
 - python에 for in과 비슷하게 객체의 필드값들에 접근가능

```javascript
var testObject = new Object();
testObject.name = 'han';
testObject.age = 30;
testObject.brith = '1992.12.12';


var key;
for(key in testObject){
    console.log(key, testObject[key]);
    //객체의 필드값들의 이름이 key 이고, 그 필드값의 이름들이 차례대로 key 변수에 들어가게됨.
    
    //그러면 testObject[key] 형식으로 각각에 key 값에 대응되는 필드값에 접근가능
}
```
<br>
<br>

## function 함수의 매개변수로 객체를 넣기
- 함수의 매개변수로 객체를 집어넣은 후, 객체의 필드값 변경
- 매개변수로 넣은 그 객체의 필드값이 변경됨.
- **객체의 참조주소가 복사**되었기 때문에 가능.
- 일반 변수를 매개변수로 넣을경우 주소가 아닌 값이 복사 되기 때문에 함수가 끝난 시점에서 매개변수로 넣은 변수의 값은 변경이 안됨.

<br>

```javascript
var a = 100;
var objA = { value : 100};
//리터럴 방법 객체생성

function change(num, obj){
    //함수의 매개변수로 객체를 집어넣어서 필드값 변경
    num = 200;
    obj.value = 200;

    console.log(num); // 200
    console.og(obj); // { value : 200 }
}

change(a, objA);

console.log(a); // 100 -> 값 변경안됨
console.loga(objA); // { value : 200 }; -> 참조된 객체의 필드값 변경 성공 

// a 값이 변경 안된 이유 : 변수의 참조 주소가 아닌, 변수의 값이 복사 되었기 때문에 a 그 자체의 값이 변경되어진게 아님.

// 반면에 objA 는 매개변수로 넣을시 객체의 참조 주소가 복사 되었기 때문에 objA 그 자체의 필드 값이 변경되어 질수 있음.
```

<br>
<br>

## 객체의 필드값 삭제하기
- 자바스크립트는 객체의 필드값을 delete 연산자로 삭제시킬수 있음
- 삭제한 필드값에 접근시에 undefined 라고 뜸
- delete 객체.필드명, 혹은 delete 객체['필드명']

```javascript
var food = {
    name : 'apple',
    price : 3000
}

delete food.name; //name 필드 삭제
console.log(food.name); //undifined
```

<br>
<br>

## 객체 끼리의 비교
- 객체 간에 비교는 참조하는 주소가 같아야 true를 반환함

```javascript
var objA = { value : 100; }
var objB = { value : 100; }

var objC = objA;

console.log(objA == objB); //false 참조 주소가 달라서 false
console.log(objC == objA); //true 참조 주소가 같음. true
```

<br>
<br>

## 프로토타입(Prototype) 객체
- 자바의 슈퍼(Super) 클래스, 부모클래스와 같다고 보면됨
- 모든 객체는 자신의 부모 객체와 연결되어있음
- 이러한 부모 객체를 프로토타입 객체 라고 부름
- **자바스크립트는 부모객체를 동적으로 바꿀수도 있음.**

- ESCMAScript 명세서에 자바스크립트의 모든 객체는 자신의 프로토 타입을 가리키는 [[Prototype]]라는 숨겨진 프로퍼티를 가진다고 함.

- 크롬 브라우저에는 __proto__가 바로 이 숨겨진 프로토타입 프로퍼티임.
  - \_\_proto\_\_ -> Object.prototype 객체
  - 객체에 관한 기본 함수들이 내장되어있음.
  - toString(), valueOf(), hasOwnProperty() ...등등

```javascript
var foo = {
    name : 'foo',
    age : 30
};

console.log(foo.toString()); //"[ojbect Object]"
// foo 객체에 toString() 함수 정의가 안되어있는데 쓸수있는 이유
// foo 객체의 프로토 타입에 toString() 이 이미 정의되어 있기 때문에 상속한것처럼 toString() 가져와서 호출 가능


console.dir(foo);
//dir(객체) -> 객체의 속성을 계층구조로 출력함.
//__proto__ 객체가 foo의 상위 계층에 숨겨져 있는것을 알수있음
//__proto__ 객체의 메소드에 toString() 이 있는것을 알수있음
//__proto__ 객체가 가리키는 객체가 Object.prototype 
//즉, Object.prototype 에서 toString()을 가져와서 씀
```

<br>
<br>
<br>
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

