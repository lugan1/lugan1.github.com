---
title: "[angular] Form Control Validiator"
tags:
- log
- angular
categories:
- angular
date: '2021-10-18 09:03:00'
classes: wide
---

# 출저 및 참고 사이트 :  
[https://angular.kr/guide/form-validation](https://angular.kr/guide/form-validation)

<br/>
<br/>

# Form Control(입력창, 카테고리 등) 유효성 검사 방법
- 보통 HTML 템플릿에서 *ng-if='조건문' 형식으로 많이 사용한다.

## Validators Class
- Form-control 에서 유효성 검사 기능을 제공한다.

|메소드|리턴값|설명|
|------|----|-----|
|**min**( min : number )|ValidatorFn|입력값이 제공된 숫자보나 크거나 같아야 하는 요효성 검사, 성공시 null, 실패시 오류맵 반환|
|**max**( max : number)|ValidatorFn|입력값이 제공된 숫자보다 작거나 같아야 하는 유효성 검사, 실패시 오류맵 반환|
|**required**( control : AbstractControl )|ValidationErrors \| null|입력값이 비어있지 않아야 할때 유효성 검사. 실패시 오류 맵 반환 |
|**requiredTrue**( control : AbstractControl )|ValidationErrors \| null |보통 체크박스에 사용되며, 입력값이 참이어야만 True, 일반적으로 필수 확인란에 사용된다. 실패시 오류 맵 반환|
|**email**( control: AbstractControl )|ValidationErrors \| null |이메일이 유효한지 유효성 검사, 유효성 검사 실패시 오류 맵 반환|
|**minLength**( minLength: number )|ValidatorFn|입력 값의 길이가 제공된 최소 길이보다 크거나 같아야 하는 유효성 검사, 예) 필드에 최소 3자가 있는지 검사. HTML5 minlength 속성을 사용하는 경우에도 기본적으로 제공된다. 유효성 검사 실패시 오류맵 반환|
|**maxLength**( maxLength: number )|ValidatorFn|입력 값의 길이가 최대 길이보다 작거나 같아야 하는 유효성 검사. 예) 필드가 최대 5자인지 확인, 실패시 오류맵 반환|
|**pattern**( pattern \| string \| RegExp)|ValidatorFn |정규식 패턴과 일치하는지 유효성 검사|
|**nullValidator**( control : AbstractControl)|ValidatorErros \| null |작업을 수행하지 않는 유효성 검사.|
|**compose**( validators : ValidatorFn\[ ])|ValidatorFn \| null |제공된 컨트롤에 대한 개별 오류맵의 합집합을 반환하는 단일 함수로 여러 유효성 검사기를 구성한다. 유효성 검사가 실패하면 유효성 검사기의 병합된 오류 맵과 함께 오류맵을 반환한다.|
|**composeAsync** ( validators : AsyncValidatorFn\[ ])|AsyncValidatorFn \| null|여러 비동기 유효성 검사기를 제공된 컨트롤에 대한 개별 오류 개체의 합집합을 반환하는 단일 함수로 구성한다. 유효성 검사가 실패하면 비동기 유효성 검사기의 병합된 오류 개체와 함께 오류 맵을 반환한다.|


## From-control 에 Validator 사용방법
- Form Builder 로 Form Group 을 빌드시에 사용할 수 있다.

사용 예제)
```typescript
FormControl : formbuilder.control('입력기본값', [
    Validator.옵션1
    Validator.옵션2
    .....
    Validator.옵션n
] )
```


