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

HttpCleint 사용, Get 요청 사용 예제)
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

