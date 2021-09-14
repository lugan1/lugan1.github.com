---
title: "[javascript] 함수 선언식 vs 함수 표현식"
tags:
- javascript
categories:
- javascript
date: '2021-09-15 03:51:57'
classes: wide
---

### 함수 선언식
```javascript
function 함수이름(){
    처리;
}
```

<br>

### 함수 표현식
```javascript
var 변수 = function(){
    처리;
}
```

<br>
<br>

## 함수 선언식과 함수 표현식의 차이
- 함수 선언식은 호이스팅 가능, 함수 표현식은 호이스팅 불가
  - 호이스팅 : 호출이 선언보다 위에 있을시 선언을 위로 끌어올림

- 함수 표현식은 클로져, 콜백으로 사용시에 유리함
  - 클로져 : 함수를 실행하기 전에 변수를 해당함수에 넘기고 싶을때 사용

- 매개변수로 함수를 넣을때 함수표현식이 유리함
