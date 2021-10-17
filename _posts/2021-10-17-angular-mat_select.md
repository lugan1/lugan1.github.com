---
title: "[angular] mat-select"
tags:
- log
- angular
categories:
- angular
date: '2021-10-17 12:31:00'
classes: wide
---
# 참고 및 출저 사이트 :  
[https://material.angular.io/components/select/overview](https://material.angular.io/components/select/overview)

<br/>
<br/>

# Material-Select
- 카테고리 같은 위젯이 필요할때 사용
- **\<mat-select> 안에 각각의 카테고리에 사용될 옵션 \<mat-option> 들이 들어간다.**
- value 속성은 카테고리를 선택했을때, 쓰여질 value 값이다.
- mat-select 에서 value 값을 설정하거나, formControlName 속성을 설정해서 카테고리의 디폴트 값을 설정할수있다.

<br/>

**FormGroup을 사용한 mat-select 사용예제**
```html
<form [formGroup] = "TS파일에서 builder로 생성한 formGroup">
<mat-select formControlName="TS파일에서 바인딩할 폼컨트롤 이름">
<mat-option value="value 값이 들어감">카테고리 텍스트</mat-option>
</mat-selct>
</form>
```

<br/>

## Mat-Select 디폴트값 설정방법
- (1)번째 방법 \<mat-select [value]="디폴트 선택 value"> \</mat-select>
- (2)번째 방법(formControl 바인딩 했을시) 
\<mat-select formControlName="폼컨트롤 이름">\</mat-select>  
====> TS파일에서 formControl 생성시의 default 값을 설정


