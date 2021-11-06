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

## **ng-if 와 ng-show 의 차이점**
- ng-show는 비교문과 상관 없이 무조건 돔을 생성한다. (ng-if 는 조건이 되어야지 생성이 된다.)
- ng-show 는 기능적으로 class="ng-hide" 클래스가 추가되어 결과적으로 display : none 스타일 속성이 추가되어 뷰에서 감춰진다.
- ng-if 는 조건문이 false 일 경우 돔을 만들지 않고, 주석문만 남겨진다.

<br/>

예시)
![ng-if_and_ng-show.png](/assets\image\posts_image\ng-if_and_ng-show.png)


<br/>

## **4. ng-class**
- Angular로 HTML 요소에 CSS 클래스를 동적으로 줄 수 있는 디렉티브다.
- ng-class "\{css속성값&class명 : 조건식}"
```html
<p ng-class="\{strike: true, bold: false, red: true}">Example</p>
```

<br/>
<br/>
<br/>


# ng-for

사용예시)
```html
<ul> 
  <li *ngFor="let hero of heroes"> \{\{ hero }} </li> 
</ul>
```
- '*' 을 사용하여 TS파일의 객체와 변수를 바인딩해서 사용할 수 있다.

- *ngFor="let 변수 of List" 형식으로 사용한다.

- 파이썬의 i in List 와 같다. List의 원소가 변수에 차례대로 들어가며, 원소의 갯수만큼 반복 실행된다.

- 해당 엘리먼트 코드블럭 \<element></element> 까지 반복실행된다. 그 안에서의 변수는 let 변수를 가져와서 사용할 수 있다.




