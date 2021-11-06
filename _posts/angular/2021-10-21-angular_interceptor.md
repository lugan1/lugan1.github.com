---
title: "[angular] Intercepter "
tags:
- log
- angular
categories:
- angular
date: '2021-10-21 10:40:00'
classes: wide
---

# Restful 에서 HTTP 통신을 주고 받는 과정
### **Front (component) <-> Front Interceptor <-> Backend Interceptor <-> Server (controller)**
- 즉 프론트와 백엔드 API 서버 둘다 Interceptor 가 있고, API 서버에서 Error code 를 응답하면 Front Interceptor 에서 체크한다.
- Font Interceptor 에서 Error code 체크후, 리다이렉트 처리를 한다.
  - Front에서 Server로 Request 할 때에도 Front Interceptor 를 거치고 나서 서버의 Interceptor 로 전달된다.

- 반대로 API 서버에서의 Interceptor 는 올바른 request 인지 확인하고 올바른 request 가 아니면 controller 를 실행 안하는 방향으로 interceptor 를 작동시킨다.
   - 예) 로그인 비밀번호가 틀림 -> interceptor false => controller 작동 x


<br/>
<br/>
<br/>

# Angular Interceptor


## Angular Interceptor 준비과정
- 프로젝트에서 Interceptor 폴더를 새로 만든다
- Interceptor service 클래스.ts를 새로 만든다.
  - Intellij 사용이면 new -> Angular Schematics -> service 를 선택하면 된다.

- @Injectable({ providedIn:'root }) 어노테이션을 적용한다.
- HttpInterceptor 를 implements 한다.
- intercept 콜백 함수를 구현한다.
   - Intellij 사용이면 Generate -> Implements Members 클릭이면 자동으로 함수가 생성된다.

- app.module.ts 파일에 생성한 Interceptor service 를 등록한다.
  - providers : 항목에 배열 형식으로 추가한다.
  - providers 는 공통적으로 사용할 Service를 등록하는 곳이다.

**app.module.ts**에 Interceptor 등록 예제)
```typescript
  providers: [
    //공통적으로 사용할 Service를 등록하는곳
    {
      provide: HTTP_INTERCEPTORS,
      useClass: 서비스 클래스명(인터셉트 클래스 이름),
      multi: true // true이면 HTTP_INTERCEPTORS 토큰으로 적용되는 인터셉터가 하나만 있는 것이 아니라, 여러 개 있다는 것을 의미한다.
    }
  ]
```


<br/>
<br/>

## angular 인터셉터 실행 순서

(AuthInterceptor, LoggingInterceptor 를 Provieders 에 등록했다고 가정)
![angular-interceptor-process.png](/assets\image\posts_image\angular-interceptor-process.png)

- 인터셉터는 Providers 에 등록된 순서대로 실행된다.
- 서버로 요청을 보내기 전에 인증 필드를 추가하고 로그를 남겨야 한다고 가정한다.
- 그러면 이 경우에는 AuthInterceptor 서비스를 Providers에 등록한 후에 그 뒤에다가 LoggingInterceptor 서비스를 등록하면 된다.
- 그러면 외부로 향하는 요청이 AuthInterceptor를 거친 후에 LoggingInterceptor 로 전달된다.
- 서버에서 돌아오는 Response 응답은 반대로 LoggingInterceptor를 거쳐서 AuthInterceptor 순으로 전달된다.
- **인터셉터를 등록한 이후에 실행 순서를 변경하거나, 특정 인터셉터를 건너띌 수는 없다.**
- **인터셉터를 적용할지 건너뛰어야 할지 지정하려면 해당 인터셉터 안에 동적으로 로직을 작성해야 한다.**

<br/>
<br/>
<br/>   

## Angular Intercptor 콜백함수 구현하기
- 다음과 같은 인터페이스 콜백 함수를 구현한다.
- 자바의 인터페이스를 @override 해서 구현하는거와 같다.

<br/>
<br/>

### intercept(httpRequest : HTTPRequest\<any\>, httpHandler: HttpHandler): Observable\<HttpEvent\<any\>\>
- intercept 메소드는 HTTP 요청을 받아서 HTTP 응답을 Observable 타입으로 반환한다.

- httpHandler 객체는 체이닝 되는 인터셉터중 다음으로 실행될 인터셉터를 의미한다.

- 그리고 인터셉터 체인중 마지막 인터셉터가 받는 httpHandler객체는 HttpClient 백엔드 핸들러이며, 이 핸들러가 실제로 HTTP 요청을 보내고 서버의 응답을 첫 번째로 받는 핸들러이다.

- 일반적으로 인터셉터는 외부로 보내는 요청에만 적용하고 HttpRequest.handle()로 받아오는 방식으로 사용한다.

- HttpRequest.handle() 이 반환하는 옵저버블을 활용하면 스트림으로 전달되는 응답 이벤트의 형태를 변환할 수 있다.



- **HttpRequest** : Interceptor 로 들어온 Request
  - 원래 request는 변경할 수 없어서 request.clone 으로 복사해야된다.
    - HttpRequest의 인스턴스와 HttpResponse 인스턴스의 프로퍼티는 readonly 이기 때문이 이뮤터블이다.
    - 앱에서 보낸 요청이 실패하면 재시도 하는 경우가 있는데, 이 때마다 인터셉터가 체이닝되면, 인터셉터가 같은 요청을 여러번 처리할 수 있기때문이다.
    - 그래서 인터셉터는 기존에 보냈던 요청은 그대로 두고, 새로운 객체를 받아서 변환 작업을 하는것이 안전하다. (clone( ) 메소드 활용)
    - 결국 인터셉터가 요청으로 보내는 객체를 한 번만 처리하는 것을 보장하기 위해 이뮤터블이 사용된다.

<br/>
<br/>

다음과 같이 request를 변경하면 error가 발생

```typescript
req.url = req.url.replace('http://', 'https://');
```

<br/>
<br/>

다음과 같이 clone({ request 변경할값 }) 사용해서 변경
```typescript
// HTTP 인스턴스을 복사하면서 'http://'를 'https://'로 변경합니다.
const secureReq = req.clone({
  url: req.url.replace('http://', 'https://')
});
// 다음 핸들러에는 수정된 인스턴스를 전달합니다.
return next.handle(secureReq);
```

<br/>

- **HttpHandler** : Http Request 를 다음 행동으로 넘기는 역활을 한다.
  - 즉, Http Request를 처리하는 기능을 담당한다.
  - HttpHandler.handle(HttpRequest).pipe() 형식으로 Request처리를 구현 한다.

<br/>
<br/>
<br/>

# Angular Interceptor로 HTTP 요청에 기본 헤더 설정하기
- AuthService : 인증 토큰을 생성
  - authService.getAuthorizationToken() : 서비스에서 인증 토큰을 가져옴 

- AuthInerceptor : 이 서비스를 주입받아 토큰을 받아오코, 애플리케이션에서 보내는 모든 HTTP요청에 인증헤더를 추가

- request.header.set('헤더에 넣을 이름', value)
- httpHandler.handle(request) : 수정한 HTTP 요청을 다음 핸들러에 전달한다.



# RxJS filter
- 소스 Observable에서 방출한 매개변수 대해서, 어떠한 조건값을 줘서 뽑아내는 함수
- 매개변수에 대한 조건값에 True를 반환하면 그 조건에 부합하는 값이 생성되고, false 이면 출력 Observable에 값이 전달되지 않는다.

- SQL의 Select Where 랑 같음. 조건에 해당되는 값만 뽑아냄
- filter(매개변수 => **매개변수에 대한** 조건식)


<br/>

# RxJS Tap
- side effect 로깅과 같은 액션을 수행
- 중간에만 빠져서 기능처리. 
- Subscribe까지는 가지 않는다. 
- 파이프에서 T자 파이프와 같은 역할
- **T자 파이프에서 l 의 역할. Subscribe로 가는 긴 파이프 통로의 흐름중에 중간에 빠져서 기능처리를 한다.**

<br/>

# RxJS catchError
- Observable 에서 Subscribe되지 못하는 Exception (error) 가 발생하면 Pipe 단계에서 Error 처리함
- HTTP ERROR 도 여기에 포함됨
- HTTP ERROR 가 발생하면 Subscribe 되지 못하는데, pipe() 에서 에러 발생을 처리한다.
- **발생한 Error 를 throw 해줘야 하는데, return throwError(error) 가 필수다.**


<br/>


## RxJS CatchError 와 Interceptor를  활용한 리다이렉트 처리 예제)

```typescript
@Injectable({
  providedIn: 'root'
})
export class ErrorInterceptorService implements HttpInterceptor{
// HTTP ERROR 발생하면 Error 코드에 따라 Interceptor 처리

  constructor(private router:Router, private dialog:MatDialog) {

  }

  intercept(httpRequest: HttpRequest<any>, httpHandler: HttpHandler): Observable<HttpEvent<any>> {


    let request: HttpRequest<any> = httpRequest.clone();
    // httpRequest를 복사해서 request 변수에 집어넣는다.

    return httpHandler.handle(request).pipe(catchError(err => {
      // catchError : Observable에서 error 가 발생하면 에러 처리. HTTP ERROR 도 여기에 들어간다.

      if (err.status == 401){
        // 에러코드가 401 (로그인 실패) 이면 다이얼로그 처리
        this.dialog.open(ResultDialog,{data:{'title':'로그인 실패', 'content':'아이디와 비밀번호를 확인해 주세요'}});
      }

      if (err.status == 403){
        // 에러코드가 403 (forbiden 권한없음) 이면 리다이렉트 처리
        this.redirect();
      }

      return throwError(err);
    }));
  }

  public redirect(): void {
    alert('로그인해야 사용할수 있습니다.');
    this.router.navigate(['/Login']);
  }

}
```

