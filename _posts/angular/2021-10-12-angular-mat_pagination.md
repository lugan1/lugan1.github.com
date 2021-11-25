---
title: "[angular, spring] 게시글 페이징 처리 Ngx-pagination"
tags:
- log
- angular
- spring
categories:
- angular
- spring
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




<br/>
<br/>


##  Mat-Table 과 Ngx-Editor 같이 사용하는 방법
- \<mat-table> 속성에 paginate: \{ } 속성을 추가한다.
- dataSource의 데이터를 TS파일에서 MatTableDataSource 가 아닌 , data: any = [];  자료형으로 바꾼다.

```html
    <!--POST 등록시 중괄호 사용시에 빌드 오류 걸려서 이스케이프 문자 \ 붙임. 실제 예제에서는 \ 제거후 사용-->
    <mat-table [dataSource]="boardList | paginate: \{itemsPerPage: 10, currentPage: page, totalItems: 100\}">

  </mat-table>
```


<br/>
<br/>
<br/>

# DB에서 원하는 데이터 섹션만 가져오기 (Paging) SQL
- Limit : 몇개 가져올건지
- Offset : 몇번 부터 해서

<br/>


끝번호부터 역순으로 10개씩 가져오는 SQL 예제)

```SQL
SELECT idx, title, writer, writeDate, hit, state 
FROM lee_board
WHERE state = 1
order by idx desc
LIMIT 10 OFFSET 0
```
- ~~HTTP GET 으로 통신하려면 Page 모델 vo 필요. (Page_LIMIT, Page_OFFSET)~~
- ~~Page 모델로 요청받고, Response 할때는 Board 모델로 응답하는 형태.~~

- GET 요청을 할때는 json body 사용은 지양 해야 한다.
- **url의 Params로 GET 요청하고, 받을때는 Board VO 모델에 메타데이터 헤더를 달아서 받는 형식**
- 메타데이터 예시) 
   - TotalCount: DB에 있는 게시글의 총 갯수
   - Offset : 어디서 부터 가져올건지
   - List\<Board> : 게시글들의 리스트

<br/>
<br/>

**Board.xml**

```xml
    <select id="selectAllPost" resultType="StudyBoard">
        SELECT idx, title, writer, writeDate, hit, state
        FROM lee_board
        WHERE state = 1
        order by idx desc
        LIMIT #{page_limit} OFFSET #{page_offset}
    </select>
```

<br/>
<br/>

# HTTP Get으로 스프링 API에서 게시글 리스트 원하는 파트만 요청 응답 (Params 이용)
- HTTP GET 통신은 BODY 사용을 지양한다.
- 앵귤러 HTTP client module 에 get요청에서 body 를 사용하는 메소드는 없고, url params 를 쓰는 건 있다.
- 따라서 API 에서도 request 를 받을때 params 로 처리하도록 했다.

<br/>

**BackBoardController.java**

```java
    @GetMapping("/getBoardList")
    public List<StudyBoard> getBoardList(@RequestParam("page_limit") int page_limit, @RequestParam("page_offset") int page_offset){
        return studyBoardService.getBoardList(page_limit, page_offset);
    }
    //게시글 리스트 조회 (page_limit, page_offset) 이용
```

<br/>

# Get으로 API에 게시글 리스트를 요청 할때는 board[] 위에 메타데이터 값을 갖는 헤더가 필요하다.
- BoardList의 VO 모델의 전체적인 모양은 이렇게 된다.
- DB에 존재하는 게시글 총 갯수. **Totalcount**
   - Totalcount 를 구하기위해, API에서는 게시글들의 총 갯수를 구하는 SQL과, 서비스 구현이 필요하다.
   - Totalcount 를 구하는 맵퍼.xml 의 resultType값은 INTGER 이여야 한다.

- 어디서 부터 짤라서 가져올건지 기준. **offset**
- Board 들의 리스트값을 넣는 **items : Board[]**

<br/>

프론트 게시글VO 예제)
```javascript
export interface Board {
  idx: number;
  title:string;
  writer:string;
  content:string;
  writeDate : string
  hit : number
}


export interface ListResponse {
  items: Board[];
  total: number;
  offset: number;
}
```

<br/>
<br/>



백엔드 게시글VO 예제)
```java
package kr.co.test.study.api.model.study;

import lombok.Builder;
import lombok.Data;

import java.util.List;

/**
 *   items: Board[];
 *   total: number;
 *   offset: number;
 */
@Data
@Builder
public class StudyBoardHeader {
    int total;
    int offset;
    List<StudyBoard> items;
    //items 에는 Board VO들의 값이 들어있는 리스트가 들어간다
}

```




<br/>
<br/>

# 프론트 Web에서 Paging 처리
- page 클릭시, TS파일에서 page_limit, page_offset 계산해서 api에 리스트 요청
- 

```html
    <div class="pagination_button_wrapper">
      <pagination-controls class="pagination_button"
                           (pageChange)="movePage($event)"
                           nextLabel="다음"
                           previousLabel="이전">
        
      </pagination-controls>
    </div>
```

<br/>
<br/>

MovePage 이벤트 처리 TS
```javascript
  movePage(page : any) : void {
    // 클릭한 page 로 url 이동

    this.page = page;
    // 하단의 page 버튼 select 상태를 클릭한 page 번호로 변경 (currnetPage : page)

    this.requestPage(page);
    //가져올 페이지의 limit와 offset 을 계산해서 API 에 게시글 리스트 요청

    this.router.navigate(['/BoardList/page', page]);
    // URL을 클릭한 page 번호로 변경
  }

    requestPage(page : any) : void{
    // 페이지 클릭시, 해당 page의 게시글을 api에 요청한다.
    // offset ~ limit 까지의 게시글을 요청한다.

    this.page_limit = 10;
    // page_limit = 10 -> 게시글을 10개씩 갖고온다

    this.page_offset = 10*(page-1);
    // offset 값은 10개씩 가져온다고 했을때 (10*(1-1), 10*(2-1), 10*(3-1)...10*(page-1)) 으로 정해진다. 10*(page-1).

    this.boardService.getBoardList(this.page_limit, this.page_offset).subscribe(data =>{
      this.boardList = data.items;
      this.listTotalCount= data.total;
    })
  }
```

<br/>
<br/>

게시글 page 리스트 조회 service.ts
```javascript
  public getBoardList(page_limit : number, page_offset : number, search?: string) : Observable<ListResponse>{

    const options = {
      params: {
        page_limit,
        // page_limit : page_limit 와 똑같은 기능. key 이름과, 매개변수의 이름이 같으면 value 를 적지 않아도 된다.
        
        page_offset,
        search: search ?? ''
      },
    };

    return this.http.get<ListResponse>('/api/api/back/board/getBoardList', options);
    // page_limit , page_offset url 파라미터로 API 에 게시글 리스트를 조회한다.
  }
```

