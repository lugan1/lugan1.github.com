---
title: "[angular] Material Table "
tags:
- log
- angular
- typescript
categories:
- angular
date: '2021-10-05 10:35:00'
classes: wide
---

## Angular Material 설치 및 App-Module 에 임포트
- [https://lugan1.github.io/angular/angular_button/](https://lugan1.github.io/angular/angular_button/) 에서 참고 후 Angular Marterial 설치

- App-module.ts 상단에 import { MatTableModule } from '@angular/material/table'; 추가
- App-module.ts 의 imports : 항목에 MaTableModule 추가

## Class is not an Angular module 뜰시에 해결방법
- [https://stackoverflow.com/questions/58437137/class-is-not-an-angular-module-only-in-intellij-webstorm-when-importing-locall](https://stackoverflow.com/questions/58437137/class-is-not-an-angular-module-only-in-intellij-webstorm-when-importing-locall)

- 왼쪽 Project Explorer 에서 Node_modules 마우스 오른쪽 클릭 -> Mark Derectory -> not excloded
- file -> invalidate caches / Restart


## HTML 파일에 MatTable 추가
```html
<mat-table [dataSource]="dataSource">
</mat-table>
```
- dataSource 속성에 dataSorce 변수를 Property 바인딩 한것
- TS 파일에서 dataSource 변수를 선언, 처리해줘야 한다.

## TS 파일에 datasource 변수 처리
```javascript
...
    consumptions = [{
        amount: 12000,
        desc: "food"
    },{
        amount: 10000,
        desc: "beverage"
    },{
        amount: 12000,
        desc: "dissert"
    }];
    dataSource = new MatTableDataSource(this.consumptions);
...
```

## HTML 파일의 \<mat-table> 태그 안에서 Column 과 Row 정의를 해준다.

```html
<p>board-list component!</p>
<mat-table [dataSource]="dataSource">
  <!-- TS 파일의 key1 : value1 , key2 : value2 형식의 배열이 datasurce 고, mat-table의 datasource 속성에 값으로 들어간다.-->

  <!-- Amount Column -->
  <ng-container matColumnDef="amount">
    <!--Data Soource 의 key 값을 적는다. amount : 1000 이면 amount 를 적는다.-->

    <!-- mat-header-cell : 제목이 들어간다.  -->
    <mat-header-cell *matHeaderCellDef> Amount </mat-header-cell>

    <!-- mat-cell : 어떤 데이터를 보여줄지를 넣는다. 변수.key 값을 적으면 해당 key 값의 value를 늘어놓는다. -->
    <mat-cell *matCellDef="let consumption"> {{consumption.amount}} </mat-cell>
    <!-- consumption 변수를 만들고, consmption.amout 값을 표시한다. 즉 key amount 의 value를 표시한다. -->

  </ng-container>

  <!-- Description Column -->
  <ng-container matColumnDef="desc">
    <mat-header-cell *matHeaderCellDef> Description </mat-header-cell>
    <mat-cell *matCellDef="let consumption"> {{consumption.desc}} </mat-cell>
  </ng-container>

  <!-- Row Template -->
  <!-- amount 와 desc를 각각 row로 설정한다. -->
  <mat-header-row *matHeaderRowDef="['amount','desc']"></mat-header-row>
  <mat-row *matRowDef="let consumption; columns: ['amount','desc'];">
  </mat-row>

</mat-table>
</mat-table>
```

실행화면)

![angular_material_table.png](/assets\image\posts_image/angular_material_table.png)



