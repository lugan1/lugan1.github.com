---
title: "[error]  Type 'AbstractControl' is missing the following properties from type 'FormControl': 해결법"
tags:
- log
- angular
- error
categories:
- angular
date: '2021-10-04 20:49:00'
classes: wide
---
# 참고 및 출저 사이트
[https://stackoverflow.com/questions/65486599/error-ts2739-type-abstractcontrol-is-missing-the-following-properties-from-ty](https://stackoverflow.com/questions/65486599/error-ts2739-type-abstractcontrol-is-missing-the-following-properties-from-ty)

<br/>
<br/>


#  Type 'AbstractControl' is missing the following properties from type 'FormControl': 

- form builder 테스트 실습 하던중에 빌드 돌리면 나오는 오류
- html파일에 [formControl]="myForm.controls['sku']" 이 구문이 문제있다고 한다
- 스택 오버플로우에 검색결과 캐스팅 오류라고 한다.
- ['controls'] 를 formControl 로 바꾸는 과정에서의 캐스팅 오류라고 한다.

# 해결법
- 오류난 구문을 다음과 같이 바꾼다

```[formControl]="$any(myForm.controls['sku'])"```
