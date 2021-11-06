---
title: "[angular] HTTP 메소드 사용하기 GET/POST "
tags:
- log
- angular
- typescript
categories:
- angular
date: '2021-10-05 11:58:00'
classes: wide
last_modified_at: '2021-10-18 04:00:00 +0900'
---

# HttpClientModule
- angular 4.3.0 버전에 추가된 모듈
- 기존에 HttpModule 이 있었지만 새로 추가된 HttpClientModule 을 사용하면 좀더 편한 방식으로 HTTP 요청을 보낼 수 있다.


# HttpClientModule 설치
- app-module.ts 의 imports : 에 HttpClientModule 을 추가한다.

## HttpCleint 사용하는 방법
- 서비스 ts에 HttpClient 를 import 한다.
- 컴포넌트에 HttpCleint 사용해도 되지만 MVVVM 모델로 사용시에 컴포넌트는 뷰 즉 보이는 작업만 하고, 기능처리, 메소드 작업은 서비스에 작성하고 서비스를 호출하는 식으로 진행한다.

<br/>

## TS파일에서 다른 TS파일(서비스) 메소드 호출하는 방법
- app-module 에 TS 클래스 import
- providers : 항목에 서비스 클래스 추가
- 예) providers : [BoardService, UserService]
```javascript
  providers: [
    //공통적으로 사용할 Service를 등록하는곳
    {
      provide: HTTP_INTERCEPTORS,
      useClass: TokenInterceptorService,
      multi: true
    }, BoardService
  ]
  ```
- service 를 사용할 컴포넌트에서 서비스 클래스를 import 한다.
- 서비스 클래스 객체를 생성한다 서비스:서비스클래스
- 컴포넌트 생성자에 service를 argument로 넣는다.
- this.서비스.메소드() 로 서비스의 메소드를 호출한다.
- PS. 앵귤러 6버전에 추가된점 : 서비스 클래스에 @Injectable({providedIn:'root'}) 를 추가하면, app-module 에 서비스를 추가 안해도 된다고 한다.

<br/>
<br/>

## HttpCleint 사용, Get 요청 사용 예제)
- **Http get 통신에서는 body를 사용하지 않는다.**
- **매개변수가 필요하면 url에 query 를 넣는 식으로 한다.**
- Http.get(url, option\{params:params}) 를 해보니 params 가 url에 쿼리 형식으로 들어갔다. 그 외에 get 옵션값에는 body 넣는것이 없다. 
- 즉 get 요청에서 매개변수가 필요한경우 url 에 매개변수를 넣어야한다.

```javascript

interface board{
  idx: number;
  title:string;
  writer:string;
  longDescription:string;
  url:string;
}
...
  getBoardList() : void{
    //get<자료형>(url) -> Observable 객체를 반환한다.
    //옵저버블은 Object 객체를 반환하며, HTTP 라이브러리에서 이 Object를 Json 파싱한다.
    //일반적으로 HTTP API 는 객체를 사용하며, 배열을 전달하지는 않는다. 배열을 전달하는 방식은 JSON 하이재킹에 대한 문제가 있기 때문이다.
    //응답으로 받은 객체를 배열로 변환 할때는 lodash에서 제공하는 values 함수를 사용한다.
    this.board = this.http.get<board[]>("/courses.json")
      .map(data => _.values(data))
      .do(console.log);
  }
```




## Property 'map' does not exist on type 'Observable<Response>' 에러 뜰시에 해결방법
- [https://stackoverflow.com/questions/37208801/property-map-does-not-exist-on-type-observableresponse](https://stackoverflow.com/questions/37208801/property-map-does-not-exist-on-type-observableresponse)

- RxJS 6.x.x 이상의 버전일경우 코드 스니펫과 같은 파이프 가능한 연산자를 사용해야 한다.

```javascript
  getBoardList() : void{
    this.http.get('https://example.com/api/items')
      .pipe(map(data => {}))
      .subscribe(result => { console.log(result); });
  }

```


## Observable 객체

참조 및 출저 사이트 :  
[https://pcconsoleoraksil.tistory.com/301?category=1080683](https://pcconsoleoraksil.tistory.com/301?category=1080683)  

- Observable :미래에 얻게 될 value/event를 가질 컬렉션.
- Observable 객체가 리턴한 값은 subscribe 를 통하여 타입별로 그 값을 읽어올 수 있다. 
- 대게 보낸 요청에 대한 응답으로 Observable 객체가 날아온다.
- 하나의 Observable 객체는 여러번 값을 리턴할 수 있다.

<br/>
<br/>

## Json 객체 얻어와서 board 자료구조에 집어넣고, console에 출력하기

```javascript
  getBoardList() : void{
    // RxJS 에서의 pipe() 함수 : 연산자를 함께 연결할 수 있다. 파이프를 사용하면 여러 기능을 단일 기능으로 결합할 수 있다.
    // 결합하려는 함수를 인수로 사용하고 실행될 때 구성된 함수를 순서대로 실행하는 새 함수를 반환한다.
    this.http.get<board[]>('/api/api/back/board/getAllPost').subscribe(data => this.board = data)
    console.log(this.board)
  }
```

<br/>
<br/>

# (21.10.06 수정) 위 방법들은 Compnent 에서 직접 HTTP 통신 처리를 할때 쓰는방법
- (API호출)->Service -> Component 순으로 MVVM 패턴을 따라 데이터를 이동하려면 비동기 처리 필요
- Promise

<br/>
<br/>
<br/>

# (21.10.18 수정) GET 요청에서 url에 Query Params 를 담아서 요청하는 방법
```typescript

//get('url', option) 에 들어갈 option 값 설정
const option = {
  params : {
    쿼리key1 : 쿼리value1,
    쿼리key2 : 쿼리value2
    ....
  }
}

http.get.('url',option)
//get 메소드의 두번째 매개변수로 앞서 생성한 option 을 집어넣는다.
```

<br/>
<br/>

**실사용 예제**
```typescript
  public getBoardList(page_limit : number, page_offset : number, search_option?: string, search_word?:string) : Observable<ListResponse>{

    // 매개변수와, value 값 이름이 같으면 key:value 를 하지 않아도, params: { 매개변수1, 매개변수2 } 형식으로 생성이 가능하다.
    const options = {
      params: {
        page_limit,
        page_offset,
        search_option: search_option ?? '',
        search_word: search_word ??''
      },
    };

    return this.http.get<ListResponse>('/api/api/back/board/getBoardList', options);
    // page_limit , page_offset url 파라미터로 API 에 게시글 리스트를 조회한다.
  }
  ```

