---
title: "[angular] Mat-Table Clcik 이벤트 구현하기"
tags:
- log
- angular
- typescript
categories:
- angular
date: '2021-10-06 14:14:00'
classes: wide
---

# 출저 및 참고 사이트 :  
[https://js2prince.tistory.com/entry/Angular-Material-Table-Event](https://js2prince.tistory.com/entry/Angular-Material-Table-Event)


<br/>
<br/>

# Angular Material Table Click Event

HTML 파일 예제)
```html
  <!-- Row Template -->
  <mat-header-row *matHeaderRowDef="['idx','title','writer','writeDate','hit']"></mat-header-row>
  <mat-row *matRowDef="let row; columns: ['idx','title','writer','writeDate','hit'];"
           class="element-row"
           (click)="onboard_detail(row)"
           
  >
    <!-- let Row로 row 이름의 객체 선언하고, (clcik) 으로 각 row 클릭시 클릭이벤트 바인딩, row 객체를 매개변수로 넘겨준다. -->
  </mat-row>
</mat-table>
```

<br/>

TS 파일
```javascript
interface Row{
    key : value
    ....
}


onboard_detail(row : Row){
    console.log(row.key) // key.value
}
```



