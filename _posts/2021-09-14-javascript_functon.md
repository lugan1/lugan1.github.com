---
title: "[javascript] 함수"
tags:
- javascript
categories:
- javascript
date: '2021-09-14 19:27:57'
classes: wide
last_modified_at: '2021-09-15 02:07:01 +0900'
---

## 기본 함수 정의문

```javascript
function 함수명(매개변수1, 매개변수2...){
    자바스크립트 코드;
}
```

<br>

## 익명함수
- 함수명이 없는 함수

```javascript
참조 변수 = fuction(매개변수1, 매개변수2...){
    자바스크립트 코드;
}
```

<br>

## 함수 호이스팅
```javascript
Func();
// 호출보다 밑에 선언하고, 호출시 밑에 선언한 함수 내용을 끌어올림

function Func() {
    자바스크립트 코드;
}
```

- 익명 함수는 호이스팅 기능일 지원하지 않음. 선언보다 호출이 앞설시에 에러발생

<br>
<br>

## 매개변수 없이 함수에 전달된 값 받아오기
- 함수 정의문에서 arguments 사용
- 매개변수를 사용하는 것처럼 함수 호출문의 값을 받아올 수 있음.

```javascript
funtion 함수명() {
    arguments; //컬렉션. 매개변수1, 매개변수2.. 의 값이 들어오게됨
}

함수명(데이터1, 데이터2 ...);




function sum() {
    var sum = arguments[0] + arguments[1] + arguments[2];
    //매개변수 1, 매개변수2, 매개변수3 의 값을 받아서 더함

    document.write(sum);
}

sum(10, 20, 30);
```

<br>
<br>

## 즉시 실행 함수
- 함수 선언과 동시에 함수 호출

```javascript
(function() {
    자바스크립트 코드;
}());
// 함수를  ( ) 으로 감싸고, 뒤에 () 추가


// function Menu A 
(function() {
    var num = 100;
    function menu(){
        num += 100;
        alert(num);
        //200 메세지의 얼럿 출력
    }
    menu();
}());


// function Menu B
(function(){
    var num 100;
    function(){
        function menu(){
            alert(num);
        }
    }
}());

// Menu A 가 먼저 실행되고, 그다음에 Menu B가 실행됨.
// 즉시 실행함수로 안하면, 함수 이름이 겹칠때, 제일 마지막에 정의된 함수만 실행됨.

```

<br>
<br>

## 객체 생성자 함수
- 객체 생성자 함수 말 그대로 객체를 생성하는 함수.
- 자바의 생성자와 비슷하다고 보면 됨
- 자바와 다른점은 function 을 생성자 필드에 넣을수 있다는게 다른점인듯

<br>

```javascript
//객체 생성자 함수
function 함수명(매개변수1, 매개변수2, ... 매개변수n){
    this.속성명 = 새 값
    this.함수명 = function(){
        자바스크립트 코드;
    }
}

var 참조변수(인스턴스 네임) = new 함수명();

var 참조변수 = { 속성 : 새 값, 함수명 : function(){ ... }}
```

<br>
<br>

생성자 함수 CheckWeight 으로 2개의 객체를 생성하는 예제 

<br>

```javascript
function CheckWeight(name, height, weight){
    this.userName = name;
    this.userHeight = height;
    this.userWeight = weight;
    this.minWeight;
    this.maxWeight;
    //여기까지는 자바와 같음


    //function getInfo(){  } 로 해도 될듯?? 차이를 모르겠음.
    // -> 밑에방식은 일종의 익명함수를 변수에 대입하는 방식.
    // 함수선언식 vs 함수표현식 차이는 호이스팅 외에 클로져사용, 콜백으로 사용등에 차이가 있음. 다음 포스트에 자세히 기재
    this.getInfo = function(){
        var str = ""
        str += "이름 : " + this.userName +",";
        str += "키 : " + this.userHeight +",";
        str += "몸무게 : " + this.userWeight +",";
        return str;
    }
    // function 을 정의해서 필드 변수에 대입 할수있음
    // getInfo() : 필드에 있는 이름, 키, 몸무게를 하나의 문자열로 합치는 함수
    


    this.getResult = function(){
        this.minWeight = (this.userHeight - 100) * 0.9 -5;
        this.maxWeight = (this.userHeight - 100) * 0.9 +5;

        if (this.userWeight >= this.minWeight && this.userWeight <= this.maxWeight){
            return "정상 몸무게 입니다";
        }
        else if(this.userWEight < this.minWeight){
            return "정상 몸무게보다 미달입니다."
        }
        else {
            return "정상 몸무게보다 초과입니다."
        }
    }
    //입력받은 몸무게를 비교하여 정상몸무게보다 초과인지 문자열 출력하는 함수


}

var jan = new CheckWeight("janbory", 168, 62);
var park = new CheckWeight("parkdaljae", 180, 88);

console.log(jan);
console.log(park);

document.write(jan.getInfo());
document.write(jan.getResult());
```

<br>
<br>

## 프로토 타입 메소드
- 객체를 생성하면 생성한만큼 객체의 등록된 함수도 같이 여러개로 생겨서, 메모리 낭비가 생김

- 프로토타입(Prototype)을 사용하여 등록한 함수는 원형(객체 생성자 함수)에서 생성된 객체를 공유할 수 있음.

- 즉, 여러개의 함수를 등록할 필요가 없음

<br>
<br>

![proto](/assets/image/posts_image/post_javasc_functon/proto1.png)

- 객체 생성마다 메서드가 생성되어 메모리 낭비가 심함


<br>
<br>
<br>

**Prototype 사용 후**

<br>

![proto2](/assets/image/posts_image/post_javasc_functon/proto2.png)

- 프로토타입을 사용하여 등록한 함수는 원형(객체 생성자 함수)에서 생성된 객체를 공유 할수 있음
- 메모리 절약 가능
- 프로토타입을 사용해 함수를 작성하면, 각 객체에 함수가 등록되지 않음. 원형 생성자에서 하나의 함수를 공유하는 것이기 때문.

<br>

사용예시)

```javascript
function 함수명(매개변수1, 매개변수2, ...매개변수 n) {
    this.속성명 = 새 값;
}

//생성자 함수명.prototype.함수명 으로 함수 작성
생성자 함수명.prototype.함수명 = function(){
    자바스크립트 코드;
}

var 참조변수 = new 함수명();
```

## 자바스크립트 내장 함수
- 자바스크립트 엔진에 내장된 함수
- 이미 내장되었기 때문에 바로 호출해서 사용 가능

<br>

**내장 함수의 종류**

|종류|설명|
|---|---|
|ecnodeURI()|문자를 유니코드 값으로 인코딩|
|encodeURIComponent()|문자를 유니코드 값으로 인코딩|
|decodeURI()|유니 코드값을 디코딩해서 다시 문자화|
|decodeURIComponent()|유니 코드값을 디코딩해서 다시 문자화|
|parseInt()|문자열 데이터를 정수형 데이터로 반환|
|parseFloat()|문자열 데이터를 실수형 데이터로 반환|
|String()|문자영 데이터로 반환|
|Number()|숫자형 데이터로 반환|
|Boolean()|논리형 데이터로 반환|
|inNaN()|숫자가 아닌 문자가 포함되어있으면 true 반환|
|eval()|문자열을 따옴표가 없는 자바스크립트 코드로 실행처리|
