---
title: "[angular] 데이터(변수) 바인딩, 메소드 바인딩 "
tags:
- log
- angular
- typescript
categories:
- angular
date: '2021-10-05 09:53:00'
classes: wide
---
# 참조 및 참고 사이트
[https://dschci.tistory.com/80?category=978065](https://dschci.tistory.com/80?category=978065)


<br/>
<br/>

# Angular 데이터 바인딩
데이터 바인딩 방법 3가지
- \$\{ 변수명 \} : String Interpolation 
- \[ 속성값 \] :  Property Binding
- ngModel

<br/>

# Angular 이벤트 바인딩
- (click)="메소드()" : Click 이벤트 바인딩

<br/>

## String Interpolation
- 단방향 데이터 바인딩
- TS파일의 변수를 HTML 템플릿으로 가져와 보여주는 것
- **$\{\{ 변수명 \}\} : String Interpolation** 형식으로 사용

<br/>

String Interpolation 사용 예제)  
TS 파일
```javascript
import { Component, OnInit } from '@angular/core';
import { Observable } from 'rxjs/Rx';

@Component({
    selector: 'app-budget',
    template: `<h3>My Budget: ₩{{budget}}</h3>`,
    styleUrls: [ './budget.component.css' ]
})
// budget 변수를 HTML template 에서 바인딩해서 사용
// 바인딩 방법 Strng interplation

export class BudgetComponent implements OnInit{
    budget: number = 0;
    ngOnInit(){
        let secondTick = Observable.timer(1000,1000);
        secondTick.subscribe((tick)=>{ this.budget += 1000; });
    }
}
```

<br/>
<br/>

## Property Binding
- 단방향 데이터 바인딩
- 태그의 속성값에 TS파일의 변수 값을 바인딩 하는 것
- 예시) **\<input type="text" [value]="budget">** 
- **[ 태그의 속성값 ] = "변수이름"** 형식으로 바인딩 한다.

<br/>

Property Binding 사용 예제)  
TS 파일
```javascript
import { Component, OnInit } from '@angular/core';
import { Observable } from 'rxjs/Rx';

@Component({
    selector: 'app-budget',
    templateUrl: './budget.component.html',
    styleUrls: [ './budget.component.css' ]
})
export class BudgetComponent implements OnInit{
    budget: number = 0;
    ngOnInit(){
        let secondTick = Observable.timer(1000,1000);
        secondTick.subscribe((tick)=>{ this.budget += 1000; });
    }
}
```

<br/>

HTML 파일
```HTML
<h3>My Budget: ₩{{budget}}</h3>
<input type="text" [value]="budget">
<!-- <input type="text" value="{{budget}}">  과 동일하다.  -->

<button>Add Income</button>
```

<br/>
<br/>

## ngModel
- 양방향 데이터 바인딩
- HTML에서 변수값 변경하면 TS 파일의 변수값도 변경되고, TS 파일의 변수값을 변경하면, HTML 파일의 변수값이 변경되는 즉 양방향으로 즉각 변수값이 반응되는 형식인듯 하다.





