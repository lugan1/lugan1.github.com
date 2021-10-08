---
title: "[angular] Promise를 이용한 Service와 Compnent의 HTTP 데이터 처리"
tags:
- log
- angular
- typescript
categories:
- angular
date: '2021-10-06 08:54:00'
classes: wide
---
# 출저 및 참고 사이트 :  
[https://programmingsummaries.tistory.com/325](https://programmingsummaries.tistory.com/325)  
[https://one-it.tistory.com/entry/Promise-%EC%A0%95%EB%A6%AC-asyncawait-%EC%82%AC%EC%9A%A9%EB%B2%95-then%EA%B3%BC%EC%9D%98-%EC%B0%A8%EC%9D%B4](https://one-it.tistory.com/entry/Promise-%EC%A0%95%EB%A6%AC-asyncawait-%EC%82%AC%EC%9A%A9%EB%B2%95-then%EA%B3%BC%EC%9D%98-%EC%B0%A8%EC%9D%B4)



# Javascirpt Pormise
- Promise 패턴을 사용하면, 비동기적인 작업들을 순서대로, 순차대로 진행하거나, 병렬로 진행할수 있게된다.
- 현재 Promise 패턴은 ECMA Script 6 스펙에 정식으로 포함되었다.


## Promise 기초 예제)
```javascript
//Promise 선언
var _promise = function (param) {

	return new Promise(function (resolve, reject) {

		// 비동기를 표현하기 위해 setTimeout 함수를 사용 
		window.setTimeout(function () {

			// 파라메터가 참이면, 
			if (param) {

				// 해결됨 
				resolve("해결 완료");
			}

			// 파라메터가 거짓이면, 
			else {

				// 실패 
				reject(Error("실패!!"));
			}
		}, 3000);
	});
};

// new Promise로 Promise 가 생성되는 직후부터 resolve 나 reject가 호출 되기 전까지의 순간을 pending 상태라고 볼 수 있다.
// 이후 비동기 작업이 마친 뒤 결과물을 약속대로 잘 줄 수 있다면

// 첫번째 파라메터로 주입되는 resolve 함수를 호출하고, 실패했다면 두번째 파라메터로 주입되는 reject 함수를 호출한다.



//Promise 실행
// _promise() 를 호출하면 Promise 객체가 리턴된다.
_promise(true)
.then(function (text) {
// Promise 객체에는 정상적으로 비동기 작업이 완료되었을때 호출하는 then 이라는 API 가 존재한다.

	// 성공시 호출할 함수
	console.log(text);
}, function (error) {
	// 실패시 호출할 함수
	console.error(error);
});


```

<br/>
<br/>

```javascript
var _promise = function (매개변수) {
    return new Promise(function (resolve, reject)) {
        비 동기적으로 동작하는 함수, 코드
    }
}


_promise(매개변수).then( { 성공시 처리함수 구현}, {실패시 처리함수 구현 } )

```

<br/>

**Primise 선언부**
- **pending** : 아직 약속을 수행 중인 상태(fullfilled 혹은 reject가 되기 전)
- **fulfilled** : 약속(promise)이 지켜진 상태
- **rejected** : 약속(promise)가 어떤 이유에서 못 지켜진 상태
- **settled** : 약속이 지켜졌든 안지켜졌든 일단 결론이 난 상태

<br/>
<br/>

## 체이닝형태로 연결된 상태에서 비동기 작업이 중간에 에러가나면 처리 Promise.catch API

<br/>
<br/>

## 여러 프로미스가 모두 완료될 때 실행 Promise.all API

<br/>
<br/>

## 프로미스의 async 와 await
- 비동기 처리르 없이 코드를 동작하면 undefined 가 출력되는 경우가 있다.
- Promise를 반환하는 함수 반환값을 사용하기 까지 **코드를 지연시키기 위해 async, await 를 사용한다.** 

Async, await 활용 예제)
```javascript
const sampleFunc = async () => {
    const result = await asyncFunc() // asyncFunc 함수는 Promise 객체를 반환한다.

    // asyncFunc() 함수의 실행결과가 반한되어 result에 할당되기 전까지, await 키워드가 console.log 함수의 실행을 지연시켜준다.

    console.log(result)

    // Proimise 객체를 반환하는 함수 asyncFunc앞에 await 를 붙이고, 이를 포함하는 함수 앞에 async를 붙여준다.

    // await 키워드를 쓰려면 반드시 async 키워드로 선언된 함수 내부여야 한다.


}
```


<br/>

## then 과 async/await 의 차이
- then : { } 코드 블록 밖의 함수는 동기화 불가
- async / await : { } 코드 블록 밖의 함수도 동기화가 진행됨
- async/await 를 사용하면 promise.then().catch() 처럼 reject를  잡아낼 수 없기 때문에 try catch 문을 사용해야 한다.



<br/>

# 출저 및 참고 사이트 :  
[https://blog.eunsatio.io/develop/Angular-HttpClient%EC%9D%98-%ED%94%84%EB%A1%9C%EB%AF%B8%EC%8A%A4%ED%99%94,-%EA%B7%B8%EB%A6%AC%EA%B3%A0-HttpInterceptor](https://blog.eunsatio.io/develop/Angular-HttpClient%EC%9D%98-%ED%94%84%EB%A1%9C%EB%AF%B8%EC%8A%A4%ED%99%94,-%EA%B7%B8%EB%A6%AC%EA%B3%A0-HttpInterceptor)

<br/>

# Angular HttpClient 라이브러리를 이용한 Promise
## 기본적인 Http 요청 예제)
```javascript
constructor(
    private http: HttpClient
) {}
 
public getData(): void {
    this.http.get('{{ request uri }}')
    .subscribe((data: any): void => {
        //do somthing with data
    }, error => {
        //handle error
    });
}
```
- subscribe 메서드를 이용해 데이터를 받아 처리
- subscribe의 두 번째 인자는 에러를 처리하는 콜백 함수
- 단점 : 콤포넌트에서 직접 Http 통신을 하는 것보다 서비스로 따로 빼서 관리하는 것이 유지보수 측면에서 좋다. (MVVM 패턴)


## 서비스에서 HTTP 메소드 처리 후, Component 로 데이터 전달
- Component를 콜백호출로 데이터 처리를 하면, 코드가 길어지니 HTTP 통신 메소드를 Promise로 만들어서 Component 에게 데이터를 전달하는 방식으로 한다.

<br/>
<br/>

## HttpClient 에서 제공하는 toPromise() 메서드 사용 예제)

Service.TS 파일
```javascript
constructor(
    private http: HttpClient
) {}
 
public async getData(): Promise<any> {
    return await this.http.get('{{ request uri }}').toPromise();
    //or return await this.http.get('{{ request uri }}').toPromise() as Data;
}
```

<br/>

Component.TS 파일
```javascript
any_service : Any_service;
this.any_service.getData().then(value => 전달받은 값 처리 구현 )

```
<br/>
<br/>

# **Promise 로 HTTP 통신을 하면 콜백 이벤트가 한번만 발생해서 (1회성), Subscribe 로 해줘야 한다.**
- Promise 는 콜백 이벤트가 한번만 발생하고, Subscribe 는 콜백이벤트가 제한없이 발생해서 HTTP 통신으로 컴포넌트에 데이터에 넘겨줄때에는 Subscribe 로 넘겨주어야 한다.

<br/>
<br/>

**앵귤러 HTTP 통신 처리과정. (Rx 패턴 사용)**

![angular_http_process.png](/assets\image\posts_image\angular_http_process.png)

<br/>

### **Http통신을 완료하고, 컴포넌트에서 subscribe로 옵저버블 객체 이벤트를 구현할때, router.navigate 로 페이지를 이동시킬 수 있다.**
```javascript
  openDeleteDialog():void{
    const dialogRef = this.dialog.open(DeleteDialog, { width: '300px', disableClose: true })
      .afterClosed()
      .subscribe(result =>{
        if(result = true){
          // 다이얼로그 응답 결과가 true, 즉 삭제 확인 버튼을 눌렀으면

          this.boardService.deleteBoard(this.postIdx).subscribe(data => { this.router.navigate(['/BoardList']) });
          // 현재 idx 게시글 수정(state=0)을 API에 요청
          // sbucribe() : HTTP 통신이 완료되면 navigate 메소드로 /boardList URL로 이동

        }
    });
```

<br/>

## 보안 문제 등으로 http request url 에 header 를 붙여서 처리하고 싶으면 HttpHeaders 모듈 사용

<br/>
<br/>

## Http 요청받으면 intercept -> 새로운 헤더를 붙여 복제 및 요청하는 방법 : HttpInterceptor

##
