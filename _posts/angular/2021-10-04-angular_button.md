---
title: "[angular] 버튼, 버튼 클릭이벤트, Angular Material"
tags:
- log
- angular
- HTML
categories:
- angular
date: '2021-10-04 03:29:00'
classes: wide
---

# 참조 및 출저 사이트
[https://copycoding.tistory.com/41](https://copycoding.tistory.com/41)  
[https://cocoder16.tistory.com/18](https://cocoder16.tistory.com/18)  
[https://webdir.tistory.com/421](https://webdir.tistory.com/421)  
[https://cocoder16.tistory.com/18](https://cocoder16.tistory.com/18)  
[https://material.angular.io/](https://material.angular.io/)

<br/>
<br/>

# 버튼(Button)

## 뷰에 버튼추가, 버튼 클릭이벤트 등록하는 방법

<br/>

**HTML 파일**
```html
<button (click)="클릭메소드이름()">버튼텍스트</button>
```

<br/>

**TS 파일**
```javascript

클릭메소드이름() : void {
    버튼클릭 이벤트 구현
}
```

<br/>
<br/>

## 버튼에 css 속성 설정 하는방법

**html 파일**
```html
<button class="이름">버튼텍스트</button>
```
<br/>

**css 파일**
```css
.버튼class이름_혹은id{
  color: brown;
  background-color: gold;
}
```


<br/>
<br/>

# Input-submit , Button-submit 차이
- Button 은 HTML5 에서 넘어오면서 버튼을 표시하기 위해 생긴 태그이다.
- Button 태그는 스스로 열고 닫을수 있어서 중간에 다른 태그들을 삽입 가능하다.
- Input 태그는 열고 닫을수 있는게 없다.


<br/>
<br/>

Input 태그 버튼과 Button 태그 버튼으로 백그라운드에 이미지 넣는 방식의 차이 예제)

<br/>

HTML
```html
<input type="button" />
<button type="button">
  <img src="http://res.publicdomainfiles.com/pdf_view/89/13942613416804.png" alt="arrow">
</button>

<button>이것을 <span>클릭</span> 해보세요.</button>


```

<br/>

CSS
```css
<!-- css -->
input {
  width: 200px; height: 200px;
  background-image: url(http://res.publicdomainfiles.com/pdf_view/89/13942613416804.png);
  background-size: 100% 100%;
}
button {
  width: 200px; height: 200px;
}
img {
  width: 100%; height: 100%;
}

span {
    color: red;
}

```

- input 태그를 사용하면, img 태그를 사용할수 없고, CSS 에서 속성을 변경해줘야 한다.

- 이미지는 img 태그를 쓰는것이 검색엔진 최적화에 도움이 되어서 Button 에서 Img 태그를 쓰는게 더 낫다.

<br/>
<br/>


## input-submit, button-submit 예제
```html
<!DOCTYPE html>
<html>
<body>

<h2>HTML Forms</h2>

<form action="/action_page.php">
  <label for="fname">test name:</label><br>
  <input type="text" id="fname" name="fname" value="John"><br>
  <label for="lname">Last name:</label><br>
  <input type="text" id="lname" name="lname" value="Doe"><br><br>
  <input type="submit" value="버튼인데 왜 input인?">
  <button type="submit">"버튼 서브밋"</button>
</form> 

<p>If you click the "Submit" button, the form-data will be sent to a page called "/action_page.php".</p>

</body>
</html>
```

<br/>

## button 의 type 속성값
- **type="submit"** : 폼의 전송 기능을 담당한다.
- **type="reset"** : 폼 작성 내용을 초기화 하는데 사용한다.
- **type="button"** : 버튼클릭 이벤트를 사용하는데 사용한다.


<br/>
<br/>
<br/>

# Angular Material
- input, button 등 여러가지 컴포넌트들의 테마 속성들을 미리 꾸며놓아논 라이브러리.
- 설치해야 사용가능
- [https://material.angular.io/](https://material.angular.io/)

<br/>

## Angular Material 설치
- Intellij 하단의 터미널 -> 커맨드 프롬프트 선택 -> 위치가 자신의 프로젝트 인지 확인
- ng add @angular/material 입력

<br/>

## Angular Material App-module 에 임포트
- app-module.ts 에 다음과 같은 내용 추가

```javascript
import { MatButtonModule} from "@angular/material/button";
import { MatIconModule} from "@angular/material/icon";


imports: 에 다음과 같은 항목 추가
    MatButtonModule,
    MatIconModule
```

<br/>
<br/>


## CSS 전역 설정에 Material 테마 관련 설정 추가, 임포트
- 전역으로 마테리얼 테마 컬러 설정
- 구글 기본제공 폰트 아이콘 임포트

<br/>

**style.css**
```css
@import "~@angular/material/prebuilt-themes/deeppurple-amber.css";
@import url("https://fonts.googleapis.com/icon?family=Material+Icons");
```

<br/>
<br/>

Angular Material 버튼 속성)

![Button_style.png](/assets\image\posts_image\button_style.png)


<br/>

|이름|설명|
|---|---|
|mat-button|사각형 버튼으로 백그라운드, 테두리 높이가 없다.|
|mat-stroked-button|사각형 버튼으로 테두리가 있고, 백그라운드, 높이가 없다.|
|mat-flat-button|사각형 버튼으로 백그라운드가 있고, 높이가 없다.|
|mat-raised-button|사각형 버튼으로 백그라운드, 테두리, 높이가 있다.|
|mat-fab|원형 버튼으로 텍스트, 아이콘을 추가할 수 있다.|
|mat-mini-fab|작은 원형 버튼으로 텍스트, 아이콘을 추가할수 있다.|
|mat-icon-button|투명한 버튼으로 아이콘을 추가할수 있다.|



<br/>
HTML 파일

```html
<button mat-button>mat_button</button>
<button mat-stroked-button>mat_stroked_button</button>
<button mat-flat-button>mat_flat_button</button>
<button mat-raised-button>mat_raised_button</button>
<button mat-fab>mat_fab</button>
<button mat-minifab>mat_mini_fab</button>
```

