---
title: "[angular] 게시글 페이징 처리 Ngx-pagination"
tags:
- log
- angular
categories:
- angular
date: '2021-10-12 11:30:00'
classes: wide
---
# 출저 및 참고 사이트 :  
[https://www.npmjs.com/package/ngx-pagination](https://www.npmjs.com/package/ngx-pagination)



# 서론
### 앵귤러 프론트 웹에서 게시글 페이징 처리를 할려고 material pagination 을 알아봤는데, 페이지의 previous, next 만 있고, 페이지를 고를 수 있는 페이지 버튼이 없어서 ngx-editor 로 알아보았다. (Angular Bootstrap 에도 페이징 처리하는 라이브러리가 있다고 한다.)


<br/>
<br/>

# Ngx-Pagination
- 프로젝트 터미널에서 다음과 같은 명령어를 입력해 ngx-pagination 모듈을 설치한다.

```
npm install ngx-pagination --save
```

- app-modules.ts의 Imports 항목에 다음과 같이 추가한다.
```javascript
imports : [ NgxPaginationModule ]
```

<br/>

# Ngx-Pagination 사용하기
## 컴포넌트 TS 파일
- TotalLength :any  변수 선언 (전체 게시글 받을 갯수)
- Page : number 변수 선언 (페이지)
- TotalLength = HTTP 통신으로 받아온 게시글 length
- HTML 템플릿에서 div 속성에 ngFor 반복문을 이용해 paginate : \{ itemPerpage : 총 페이지, currentPage : 현재페이지, totalItems:받아온 게시글 총갯수 \} 를 작성한다.
- HTML 템플릿에서 페이지네이션 컨트롤을 작성한다.
```html
<pagination-controls (pageChange)="p = $event"><pagination-controls>
```


<br/>
<br/>

## ngx-pagination 예제 소스

TS파일 소스    
```javascript
export class MyComponent {
    p: number = 1;
    collection: any[] = someArrayOfThings;  
}
```

HTML파일 소스
```HTML
    <ul>
      <li *ngFor="let item of collection | paginate: { itemsPerPage: 10, currentPage: p }"> ... </li>
    </ul>

     <pagination-controls (pageChange)="p = $event"></pagination-controls>
```

<br/>
<br/>

## PaginationControl 속성
```html
<pagination-controls  id="some_id"
                      (pageChange)="pageChanged($event)"
                      (pageBoundsCorrection)="pageChanged($event)"
                      maxSize="9"
                      directionLinks="true"
                      autoHide="true"
                      responsive="true"
                      previousLabel="Previous"
                      nextLabel="Next"
                      screenReaderPaginationLabel="Pagination"
                      screenReaderPageLabel="page"
                      screenReaderCurrentLabel="You're on page">
</pagination-controls>
```


- **id** \[string]: 한 번에 둘 이상의 페이지 매김 인스턴스를 지원해야 하는 경우 ID를 설정하고 PaginatePipe 구성에 설정된 ID와 일치하는지 확인하십시오.


- **pageChagne** \[event handler]: 지정된 식은 페이지 매김 컨트롤 중 하나를 클릭하여 페이지가 변경될 때마다 호출됩니다. $event 인수는 새 페이지의 번호가 됩니다. 이것은 PaginatePipe에 전달된 currentPage 변수의 값을 업데이트하는 데 사용해야 합니다.
  - pageChange ="페이지 클릭시 처리메소드 ($event)"
  - 매개변수 $event : 페이지 클릭했을때의 번호. next 누르면 next 클릭했을때의 이동할 page 번호



- **pageBoundsCorrection** \[evnet handler] : 지정된 표현식은 currentPage 값이 범위를 벗어났을 때 호출됩니다(예: 컬렉션 크기 감소). $event 인수는 가장 가까운 유효한 페이지의 번호입니다.


- **maxSize** \[number] : 표시할 최대 페이지 링크 수를 정의합니다. 기본값은 7입니다.

- **directionLinks** \[bollean] : false로 설정하면 "이전" 및 "다음" 링크가 표시되지 않습니다. 기본값은 true입니다.


- **autoHide** \[boolean] : true로 설정하면 컬렉션의 모든 항목이 첫 번째 페이지에 맞을 때 페이지 매김 컨트롤이 표시되지 않습니다. 기본값은 false 입니다.

- **responsive** \[boolean] : true로 설정하면 개별 페이지 링크가 작은 화면에 표시되지 않습니다. 기본값은 false 입니다.

- **previousLabel** \[string] : "이전" 링크에 표시된 레이블입니다.

- **nextLabel** \[string]: "다음" 링크에 표시되는 레이블입니다.

- **screenReaderPaginationLabel** \[string] : 화면 판독기용 컨트롤에 레이블을 지정하는 데 사용되는 "페이지 매김"이라는 단어입니다.

- **screenReaderPageLabel** \[string] : 스크린 리더용으로 생성된 특정 문자열에 사용되는 "페이지"에 대한 단어, 예: "다음 페이지".

- **screenReaderCurrentLabel** \[string] : 화면 판독기의 현재 페이지를 나타내는 문구, 예: "페이지에 있습니다".







##  Mat-Table 과 Ngx-Editor 같이 사용하는 방법
- \<mat-table> 속성에 paginate: \{ } 속성을 추가한다.
- dataSource의 데이터를 TS파일에서 MatTableDataSource 가 아닌 , data: any = [];  자료형으로 바꾼다.



### SQL
- Limit : 몇개 가져올건지
- offset : 몇번 부터 해서

<br/>


끝번호부터 역순으로 10개씩 가져오는 SQL 예제)

```SQL
        select R1.* FROM(
            SELECT idx, title, writer, writeDate, hit, state 
            FROM lee_board
            WHERE state = 1) R1
        order by idx desc
        LIMIT 10 OFFSET 0
```