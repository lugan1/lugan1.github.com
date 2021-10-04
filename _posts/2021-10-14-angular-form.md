---
title: "[angular] Form 태그, Angular Form"
tags:
- log
- angular
- HTML
categories:
- angular
date: '2021-10-04 11:02:00'
classes: wide
---

# 출저 및 참고 사이트
[https://cocoder16.tistory.com/17?category=1173631](https://cocoder16.tistory.com/17?category=1173631)  
[https://m.blog.naver.com/edy5016/221278396941](https://m.blog.naver.com/edy5016/221278396941)


<br/>
<br/>

# \<Form> 태그
- \<input> 태그를 입력하면 사용자가 데이터를 입력할 수 있다.
- **\<Form> 태그**를 이용하면 입력받은 데이터를 목적지 HTML page, 혹은 서버로 전송할 수 있다.

<br/>

## \<Form> 태그 이용 Login 기본 예제

<br/>

### Form 태그 속성값
- **action** : 폼 데이터가 전송되는 요청 주소인 url
- **name** : 스크립트나 서버에서 폼을 식별하기 위해 사용하는 폼의 이름
- **method** : HTTP 메소드를 설정. GET/POST 등등

**index.html**
```html
<form action="./result.html" name="loginForm" method="get">
    <p>id: <input type="text" name="id" /></p>
    <p>password: <input type="password" name="password" /></p>
    <input type="submit" value="log in" />
</form>
```

<br/>

**result.html**
```html
<span>login succeeded</span>
```

## Form 태그 전송 결과 확인 하는 방법
### (1). 크롬 개발자 메뉴 -> Network 탭
### (2). Form 태그로 전송 누르고 General 탭에서 상세 확인가능

<br/>
<br/>
<br/>

# Angular Form
- 앵귤러는 Form 관련해서 다양한 도구들을 제공한다.
- **Form Control** : 폼에 입력된 내용을 캡슐화 하고, 이를 처리할 수 있는 객체를 제공한다.
- **Validator** : 일정 방식에 따라 입력 내용을 검증한다. (정규식 검사할때 유용할 듯)
- **Observer** : 폼의 입력창을 주시하다가, 변경 내용에 맞춰서 반응한다.

<br/>

## From Control
- 입력필드 하나를 나타낸다.
- 앵귤러 폼에서 가장 작은 단위다.
- 필드의 값을 캡슐화 하고, 이 값이 유효한지, 혹은 변경되었는지, 오류가 있는지 적시한다.

FormContorl 객체 사용 예제)  
TS 파일
```javascript
// "Nate" 라는 이름으로 새로운 FormContorl 생성
let nameContorl = new FormControl("Nate");

let name = nameContorl.value; // -> Nate;

// 이제 이 컨트롤의 값을 조회할 수 있다.
nameControl.errors // -> StringMapn<string, any> 등의 오류
nameControl.dirty // -> false
nameContorl.valid // -> true
```

HTML 파일
```html
<!-- HTML 파일에 폼 컨트롤 바인딩하기 -->
<input type="text" [formContorl]="name"/>
```

<br/>
<br/>

## Form Group
- 여러개의 Form Control 을 다룰때 사용한다.
- 여러 Form Control 에 래퍼 인터페이스(warpper interface)를 둔다.


```javascript
let psersonInfo = new FormGroup({
    firstName : new FormControl("Nate"),
    lastName : new FormControl("Murray"),
    zip : new FormControl("90210")

})

//FormGroup 과 FormControl 은 조상이 같아서(AbstarctControl) 같은 status나 value 메소드를 사용할 수 있다.
personInfo.value;
// {
// firstName : "Nate",
// lastName : "Murray",
// zip : "90210"
// }

psersonInfo.errors // -> StringManp<string, any> of errors
psersonInfo.dirty // -> false
psersonInfo.valid // -> true
```

<br/>
<br/>

## Forms Module
- 다음과 같은 템플릿 방식의 지시자를 사용한다
- ngModel
- NgForm
- Forms Module 을 임포트하면, 자동으로 모든 Form 태그문에 ngForm 이 사용된다.
- 하지만 특별하게 매개변수에 지시할수있다. \<form #myform="ngForm"> 처럼 속성값을 줄수있다. 이렇게 하면 **TS 파일에 myform 변수로 ngForm 을 매개변수로 줄수 있게됨.**
- **NgForm 은 formGroup 이 포함된 \</form> 에는 적용되지 않는다.**


## Reactive Forms Module
- 다음과 같은 지시자들을 사용한다
- formControl
- ngFormGroup
- 복잡한 폼 구성이 필요할 때 사용


## NgModule 임포트하는 방법
- app.modules.ts 에 다음과 같은 내용을 추가한다.

```javascript
imports : [
    FormsModule, // --> 추가
    ReactiveFormsModule // --> 추가
]
```

<br/>
<br/>

**단순 SKU폼 예제**

ts파일
```javascript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-demo-form-sku',
  templateUrl: './demo-form-sku.component.html',
  styleUrls: ['./demo-form-sku.component.scss']
})
export class DemoFormSkuComponent implements OnInit {

  constructor() { }

  ngOnInit(): void {
  }


  onSubmit(form: any) : void {
    console.log("you submitted value:", form);
    //you submitted value: {sku: "sku"}
    //you submitted value: {sku: "asdf"}

  }

}
```

HTML파일

```html
<div class="ui raised sgment">
  <h2 class="ui header">Demo Form: Sku</h2>

  <!-- #v = "thing" 지역변수를 만들겠다는 문법 -->
  <!-- 변수 #myform 에 바인딩되어 사용할 ngForm 앨리어스를 만듬. 즉 #myform 별칭을 ngForm 으로 지정한거임-->
  <!-- ngForm 은 NgForm 의 지시자여서 뷰에서 myform을 FormGroup 객체로 사용할 수 있게됨-->
  <!-- (ngSubmit)  부분은 NgForm 에서 만들어졌고, ngSubmit 동작을 바인딩함-->
  <!-- (ngSubmit) ="제출할때의 구현함수()" -->
  <!-- 매개변수 myform 은 위에서 지정한 FormGroup(ngForm) 이고, myform.value는 FormGroup의 키,값 쌍을 반환한다. -->
  <form #myform="ngForm"
        (ngSubmit)="onSubmit(myform.value)"
        class="ui form">

    <div class="field">
      <!--placeholder : 텍스트 입력창이 비었을때 나나타는 힌트 -->
      <!--ngModel : ngModel 의 selector를 지정한다. ngModel ="whatever" 같은 속성을 둘수 있다. 여기서는 속성값지정을 안했다.-->
      <!--ngModel 을 속성값 지정 안하면 다음과 같이 사용된다. 1. 단방향 데이터 바인딩, 2. 이 폼에 sku 라는 이름으로 만들어질 FormControl (name : sku)-->
      <!-- sku 라는 이름으로 formControl 이 만들어져서 form Group에 추가된다.-->
      <input type ="text"
             id = "skuInput"
             placeholder = "SKU"
             name = "sku"
             ngModel>
    </div>

    <button type="submit" class="ui button">Submit</button>
  </form>
</div>

```
<br/>

### 실행화면
![form_sku.png](/assets\image\posts_image\form_sku.png)


<br/>
<br/>

## Form Builder
- Form 작성을 도와주는 도우미 클래스
- 폼은 Form Control 과 Form Group 으로 구성되며 Form builder 가 생성해준다.
- 컴포넌트 TS파일에 다음과 같이 import를 추가해주어야 한다.
```javascript
import {
  FormBuilder,
  FormGroup
} from '@angular/forms';
```

<br/>
<br/>

**Form Builder 예제**

TS파일
```javascript
import { Component, OnInit } from '@angular/core';
import {
  FormBuilder,
  FormGroup
} from '@angular/forms';


@Component({
  selector: 'app-demo-form-reactive',
  templateUrl: './demo-form-reactive.component.html',
  styleUrls: ['./demo-form-reactive.component.scss']
})
export class DemoFormReactiveComponent implements OnInit {
  myForm: FormGroup;

  constructor(formbuilder: FormBuilder) {
    //Formbuilder.group() -> 새로운 FormGroup 을 만든다. 파라미터 [key: string]: any
    //Formbulder.control() -> 새로운 FormControl 을 만든다.
    this.myForm = formbuilder.group({
      'sku' : ['ABC123']
    })
    // sku 라는 컨트롤을 하나 설정했고, 그 값은 ABC123 이다. 즉 설정된 컨트롤의 기본값도 ABC123 이다.

  }

  ngOnInit(): void {
  }

  onSubmit(value: string) : void {
    console.log('you submitted value : ', value);
  }
}
```

HTML파일
```html
<div clas="ui raised sgment">
  <h2 class="ui header">Demo Form: Sku with Builder</h2>

  <!-- [formGroup]="myForm" -> myForm 을 이폼의 FormGroup 으로 사용한다-->
  <form [formGroup]="myForm"
        (ngSubmit)="onSubmit(myForm.value)"
        class="ui form">

    <div class="field">
      <input type="text"
             id="skuInput"
             placeholder="SKU"
             [formControl]="$any(myForm.controls['sku'])">
      <!--[formControl]="$any(myForm.controls['sku'])"   -> 기존의 Formcontrol 을 input에 바인딩한다. -->
      <!-- TS 파일에서 sku : ABC123 으로 control 을 생성했다. 그거를 input 에다가 바인딩 하는것-->
    </div>

    <button type="submit" class="ui button">Submit</button>

  </form>
</div>
```

<br/>

### 실행화면

![angular_formbuilder.png](/assets\image\posts_image\angular_formbuilder.png)