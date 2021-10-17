---
title: "[angular] ng-deep, ng-if, ng-switch, ng-for"
tags:
- log
- angular
categories:
- angular
date: '2021-10-18 04:13:00'
classes: wide
---

# ng-deep

# 출저 및 참고 :  
[https://angular.kr/guide/component-styles](https://angular.kr/guide/component-styles)

<br/>

- 컴포넌트의 스타일을 지정할때 사용
- Angular Material 의 스타일을 지정할 수 있다.
- 곧 지원 중단될 예정이라고 한다.
- 컴포넌트가 위치하는곳에 스타일을 적용할려면 :host, 컴포넌트 밖의 위치하는 곳에 스타일을 적용할려면 :host-context 가 좋다고 한다.


사용예제) <br/>
**mat-card의 외곽선을 style 할수 있다.**
```css
::ng-deep .mat-card_join{
  border: 1px solid #000;
}
```

<br/>
<br/>
<br/>


# Angular JS 조건문
- 해당 속성을 사용한 element 태그가 조건에 따라서 실행, 비실행된다.
- ng-switch
- ng-if
- ng-hide, ng-show
- ng-class
- \*ng-if, \*ng-switch 등 '*'을 앞에 첨부하면 TS파일의 객체, 변수들을 바인딩해서 조건식에 쓸수 있다.


<br/>
<br/>

## **1. ng-switch**
- 해당 조건에 따라서 태그가 실행된다.
- **ng-switch on="base 변수"**
- **ng-switch-when="base 변수에 대한 조건식"**
- **ng-switch-when-default 디폴트값 (아무 조건도 걸리는것이 없으면 해당 태그가 실행된다)**

<br/>

사용 예제)
```html
<div ng-switch on="name">
  <div ng-switch-when="HONG">
    <!-- name 값이 HONG 일 때 해당 태그가 실행된다. -->
  </div>
    <div ng-switch-default>
      <!-- default -->
    </div>
</div>
```

<br/>

## **2. ng-if**
- **ng-if="조건식"**
- if/else 는 제공하지 않는다. 오로직 if 문만 사용

```html
//변수 name이 may라면 태그 보여짐 
<div ng-if="name == may">
    메이의 블로그
</div>

//변수 title이 angularjs라면 태그 보여짐
<div ng-if="title == angularjs">
     angularjs 공부
</div>
```

<br/>

## **3. ng-hide / ng-show**
- ng-hide="조건식"
- ng-show="조건식"

```html
<div ng-show="true">
  true면 표시된다
</div>

<div ng-hide="false">
  false면 hide 된다.
</div>
```

<br/>

## **4. ng-class**
- Angular로 HTML 요소에 CSS 클래스를 동적으로 줄 수 있는 디렉티브다.
- ng-class "\{css속성값&class명 : 조건식}"
```html
<p ng-class="{strike: true, bold: false, red: true}">Example</p>
```




# ng-for




