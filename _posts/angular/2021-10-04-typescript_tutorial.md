---
title: "[angular] 타입 스크립트 타입선언"
tags:
- log
- angular
- typescript
categories:
- angular
date: '2021-10-04 01:20:00'
classes: wide
---

# 참고 및 출저 사이트
[https://velog.io/@recordboy/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8TypeScript-%ED%83%80%EC%9E%85-%EC%84%A0%EC%96%B8](https://velog.io/@recordboy/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8TypeScript-%ED%83%80%EC%9E%85-%EC%84%A0%EC%96%B8)

<br/>
<br/>

# 타입스크립트 타입선언
- 변수명 : 자료형 = value 형식으로 자료형 변수를 선언한다.  

<br/>

## 자료형 선언 예제)

```javascript
let a: string = 'text'; // 문자열
let b: number = 0; // 숫자형
let c: boolean = true; // 논리형
let d: any = true; // 어떤 타입이 올지 모를 때
let e: string | number = '0'; // 문자열이나 숫자가 올 때


// 자료형과 맞지 않는 값을 대입시에 에러 발생
let a: string = 0; // error
```

<br/>
<br/>

## 타입 종류

|Type|설명|
|----|----|
|boolean|true와 false|
|null|값이 없다는 것을 명시한다.|
|undefined|값이 할당되지 않은 변수의 초기값|
|number|숫자|
|string|문자열|
|symbol|고유하고 수정 불가능한 데이터타입이며 주로 객체의 프로퍼티로 식별자로 사용한다.(ES6에서 추가됨)|
|object|객체형(참조형)|
|array|배열|
|tuple|고정된 요소수 만큼 타입을 미리 선언후 배열을 표현|
|enum|열거형, 숫자값 집합에 이름을 지정한 것|
|any|타입 추론 할수 없거나 타입 체크가 필요없는 변수에 사용한다. var 변수와 같이 어떤 타입의 값이라도 할당 가능하다.|
|void|일반적인 함수에서 반환값이 없는 경우 사용한다.|
|never|결코 발생하지 않는 값|

<br/>
<br/>

## 배열선언 예제)
```javascript
// 문자열만 가지는 배열
let arr01: string[] = ['a', 'b', 'c'];
let arr02: Array<string> = ['a', 'b', 'c'];

// 숫자형만 가지는 배열
let arr03: number[] = [1, 2, 3];
let arr04: Array<number> = [1, 2, 3];

// Union 타입(다중 타입)의 문자열과 숫자를 동시에 가지는 배열
let arr05: (string | number)[] = [1, 'a', 2, 'b', 'c', 3];
let arr06: Array<string | number> = [1, 'a', 2, 'b', 'c', 3];

// 배열이 가지는 값의 타입을 추측할 수 없을 때 any를 사용할 수 있다.
let arr07: (any)[] = [1, 'a', 2, 'b', 'c', 3];
let arr08: Array<any> = [1, 'a', 2, 'b', 'c', 3];
```

<br/>
<br/>

## 함수선언 예제)
```javascript
function sum(a: number, b: number): number {
  return a + b;
}
console.log(sum(2, 3)); // 5
```

<br/>
<br/>

## 객체 선언 예제)
```javascript
let obj: object = {};
let arr: object = [];
let func: object = function() {};
let date: object = new Date();


let user: { name: string, age: number } = {
  name: 'a',
  age: 20
};
console.log(user); // {name: "a", age: 20}

```

