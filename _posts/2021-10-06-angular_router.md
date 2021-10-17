---
title: "[angular] Component 간에 페이지(page) 이동하기 (router)"
tags:
- log
- angular
- typescript
categories:
- angular
date: '2021-10-06 14:41:00'
classes: wide
last_modified_at: '2021-10-17 14:02:01 +0900'
---





# Angular Routing
- 홈페이지 작업시 프론트 엔드에서 기능해야할 필수 요소중 하나
- 과거엔 \<a> 태그로 하이퍼링크 달면 페이지 이동이 간단하게 구현되었지만, 컴포넌트간의 이동은 Angaulr 프레임워크로 구현한다.

- Angular 프레임워크는 최초에 필요한 모듈과 필요한 서비스를 전부 들고 온 다음에, Routing 기능을 통해서 필요한 View 화면만을 불러와 기능하게 한다.

- 페이지 이동시 Back 버튼 이동으로 History를 어떻게 구현해야될지 생각해야된다.

- 딥링킹(Deep Linking) 이슈도 생각해야 한다. 예) http://blog.asdf.co.kr/list?category=1234" 같이 이런 파라미터에도 매개변수로 이동 할수 있도록 기능을 제공해야된다.

<br/>
<br/>

## app-module.ts 에 Router 임포트
- imports: 속성에 AppRoutingModule 을 추가한다.

<br/>
<br/>


## AppRoutingModule 클래스를 새로 생성한다.

```javascript
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router'; // 라우터 관련 심볼을 로드합니다.

const routes: Routes = []; // 라우팅 규칙은 이 배열에 등록합니다.

// NgModule의 imports, exports 배열에 RouterModule을 등록합니다.
@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

<br/>
<br/>

## 라우팅 규칙을 Routes 배열에 등록한다.
```javascript
const routes: Routes = [
  { path: 'first-component', component: FirstComponent },
  { path: 'second-component', component: SecondComponent },
];
// path : 라우팅 규칙에 해당하는 URL 주소를 지정한다.
// 예) loaclhost:4200/first-component
// 예) localhost:4200/secont-component

// component : 해당 URL 주소에 연결될 컴포넌트를 지정한다.

...

export class AppRoutingModule{

}
```

## 라우팅 규칙을 애플리케이션에 등록한다.
- 클릭 링크를 걸 HTML 파일에 라우트 속성의 \<a> 태그를 등록한다.


```html
<p>main-component!</p>
<h1>Angular Router App</h1>
<!-- 아래 링크를 클릭하면 AppRoutingModule에 등록된 라우팅 규칙에 따라 화면을 전환합니다. -->
<nav>
  <ul>
    <li><a routerLink="/first-component" routerLinkActive="active">First Component</a></li>
    <li><a routerLink="/second-component" routerLinkActive="active">Second Component</a></li>
  </ul>
</nav>
<!-- 라우팅된 화면은 <router-outlet> 위치에 표시됩니다. -->
<router-outlet></router-outlet>
<p>main-component end!</p>
```

<br/>
<br/>

실행화면)  

![angular_router1.png](/assets\image\posts_image\angular_router1.png)

- 클릭시 해당 컴포넌트 url로 이동되며 페이지가 이동되는 것이 아니고 컴포넌트가 \<app-main> \<app-main> 태그 안쪽에 펼쳐진다.

<br/>
<br/>
<br/>

# 라우팅 규칙으로 페이지 이동시에 정보(변수) 전달하는 방법
## ActivatedRoute 인터페이스 활용
### (1) 이동할 Component TS파일에 Router, ActivatedRoute, ParamMap 을 임포트한다.
```javascript
import { Router, ActivatedRoute, ParamMap } from '@angular/router';
```


### (2) 생성자에 ActivateRoute 인스턴스를 의존성으로 주입한다.
```javascript
constructor(
  private route: ActivatedRoute,
) {}
```

### (3) 생성자에 ActivatedRoute 객체안에 있는 id 인자를 참조한다.
```javascript
ngOnInit() {
  this.route.queryParams.subscribe(params => {
    this.id = params['id'];
  });
}
```


전체코드)
```javascript
import { Component, OnInit } from '@angular/core';
import { Router, ActivatedRoute, ParamMap } from '@angular/router';

@Component({
  selector: 'app-board-detail',
  templateUrl: './board-detail.component.html',
  styleUrls: ['./board-detail.component.scss']
})
export class BoardDetailComponent implements OnInit {

  id : any | undefined;

  constructor(private route : ActivatedRoute) {

  }



  ngOnInit(): void {
    this.route.queryParams.subscribe(params => {
      this.idx = params['idx'];
    });
  }
}
```

<br/>
<br/>


# URL의 쿼리 인자, 변수값 TS파일로 갖고 오는 방법
### (1). app-routing.module 에 라우팅 규칙을 추가한다
```javascript
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import {MainComponent} from "./page/main/main.component";
import {BoardDetailComponent} from "./page/board-detail/board-detail.component";
import {BoardListComponent} from "./page/board-list/board-list.component";
 // 라우터 관련 심볼을 로드합니다.



const routes: Routes = [
  {
    path: '',
    component: MainComponent
  },
  {
    path: 'detail/:idx',
    component: BoardDetailComponent
    // :(입력받을 변수)
  },
  {
    path: 'BoardList',
    component: BoardListComponent
  }
];

// NgModule의 imports, exports 배열에 RouterModule을 등록합니다.
@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

<br/>

### (2). 라우터 이동 이벤트에 변수 값을 등록한다.
```javascript
[routerLink]="['/BoardList', 'detail', row.idx]"
//이러면 라우터 이동시에 boardList/detail/(row.idx) 값으로 이동되어진다.
// [ruouterLintk]= [url주소, 하위url주소, 하위url 주소 형식으로 매개변수값이 되어진다. 즉 url dpeth 지정가능

```

<br/>

### (3.) TS 파일에서 URL의 변수값을 가져온다.
- this.route.snapshot.params["(가져올 변수명)"] 사용

```javascript
import { Component, OnInit } from '@angular/core';
import { Router, ActivatedRoute, ParamMap } from '@angular/router';

@Component({
  selector: 'app-board-detail',
  templateUrl: './board-detail.component.html',
  styleUrls: ['./board-detail.component.scss']
})
export class BoardDetailComponent implements OnInit {

  postIdx : number | undefined;


  constructor(private route : ActivatedRoute) {
    this.postIdx = this.route.snapshot.params["idx"]
  }


  ngOnInit(): void {
    console.log("idx 변수값 : "+this.postIdx);
  }

}
```


<br/>

# 자식 라우팅 규칙 적용하기
- 애플리케이션이 점점 복잡해지다 보면 특정 컴포넌트 안에서 동작하는 라우팅 규칙을 추가하고 싶은 경우도 있다.
- 이렇게 중첩된 라우팅 규칙을 **자식 라우팅 규칙(child route)**이라고 한다.
- 라우팅 규칙을 중첩해서 적용하려면 컴포넌트에 \<router-outlet>을 더 추가해야 한다.
- 왜냐하면 첫번째 계층에서 동작하는 라우팅 규칙은 AppComponent의 \<router-outlet>안에서 동작하기 때문이다.
- 자식 라우팅은 페이지 이동이 아니고 컴포넌트가 컴포넌트 아래에 열리는 식으로 작동된다.
- 예) 블로그에서 카테고리 선택하면 하위 카테고리 열리는 형식

## 첫번째로 이동할 라우팅 HTML 파일에 다음과 같이 작성한다.
```html
<h2>First Component</h2>

<nav>
  <ul>
    <li><a routerLink="child-a">Child A</a></li>
    <li><a routerLink="child-b">Child B</a></li>
  </ul>
</nav>

<router-outlet></router-outlet>
```

## 그 다음에 AppRoutingModule TS파일에 다음과 같이 작성한다.
- 자식 컴포넌트로 이동할 라우팅 규칙 추가
```javascript
const routes: Routes = [
  {
    path: 'first-component',
    component: FirstComponent, // 이 컴포넌트 템플릿에 <router-outlet>이 존재합니다.
    children: 
      [
        {
        path: 'child-a', // 자식 라우팅 규칙과 연결되는 주소
        component: SecondComponent, // 라우터가 렌더링하는 자식 컴포넌트
        }
      ],
  },
];
```

<br/>

실행화면)

![angular_router2.png](/assets\image\posts_image\angular_router2.png)

- First Component 를 클릭하면 First Component 가 펼쳐지고, child A 를 클릭하면 Child A 컴포넌트가 그 아래에 펼쳐지는 형태.
- url 주소 : http://localhost:4200/first-component/child-a

- 아직까지 페이지 이동은 아니다.


- **페이지 이동 하려면 HTML 템플렛에 \<component>\</component> 대신 \<router-outlet>\</router-outlet> 으로 작성해야 한다.**

- **최상위 HTML 에다가 \<router-outlet>


<br/>
<br/>
<br/>

# URL 디자인 방법
## 1. Path Variable
- 가공되지 않은 정적 자원을 특정해서 보여줄때 사용.
- 예) users/1234
- 특정 자원에 대한, 어떤것을 하자는 동사는 빠져있는데 그 역할을 하는 것이 HTTP 메소드이다.

<br/>

## 2. Query Params
- 어떤 자원을 재가공해서 정렬하거나, 필터링 해서 보여줄때,매개변수를 URL에 담아서 back end 에 보낼때 사용한다.
- Path Variable 방식도 JSON 객체에 매개변수를 담아서 back end 에 보내줄 수 있지만, GET방식을 사용시에 JSON BODY를 담아서 보내는 방식은 지양해야되서 보통 Query Params 를 많이 사용한다.

- 예) BoardList?page=1&option=content&word=testword

<br/>

## 3. URL에서 동사는 사용하지 않는 것이 좋다.

## 4. 변수가 앞에오고, 그 뒤에 변수를 수식하는 단어가 오는것이 좋다.

예)BoardList/modify/:idx 형식이 아닌 BoardList/:idx/editor 형식으로. 페이지 번호가 앞에오고, 그뒤에 수식자가 옴


<br/>
<br/>
<br/>

# Angular Query Parms 방법으로 URL 라우팅하는 방법
## 참고 및 출저 :  
[https://www.digitalocean.com/community/tutorials/angular-query-parameters](https://www.digitalocean.com/community/tutorials/angular-query-parameters)

----------------------------------------------

<br/>

<br/>

## app-routing-modules.ts 에 다음과 같이 설정한다.

<br/>

**app-routing-modules.ts**
```typescript
const routes: Routes = [
  { path: '', component: MainComponent },
  { path: 'BoardList', component: BoardListComponent }
```

- 즉 BoardList 에 대한 Query를 하겠다는 것이다.
- BoardList?page=1 이런식으로 Query 한다.  

<br/>

## URL을 라우팅할 이벤트에 BoardList URL에 대한 queryParmas 를 지정한다.

- 예)

```typescript
router.navigate['Base URL 주소'], \{queryParams:}\{ 쿼리할key:쿼리value, 쿼리할key2:쿼리value2 ...}
```


<br/>


**BoardList.ts**
```typescript
this.router.navigate(['/BoardList'], {queryParams:{ page : this.page, search_option : this.FC_search_option, search_word : this.FC_search_word }});
    // URL을 클릭한 page 번호로 변경
```
- 이벤트 발동시 **BoardList?page=1&search_option='title'&search_word='테스트'** 형식으로 Routing 된다.

<br/>

-----------------------------------------


<br/>
<br/>

## queryParams URL 에서 매개변수의 값을 가져오는 방법
- **activatedRoute.snapshot.queryParams** 사용

예)
```typescript
this.page = activatedRoute.snapshot.queryParams['page'] ?? 1;
// URL에서 BoardList?page=1 이면 'page' 에 해당하는 매개변수 값을 this.page 에 집어넣는다. null 값이면 1을 집어넣는다.
```

<br/>

## ActivatedRoute 객체
### 공홈 API 문서
[https://angular.kr/api/router/ActivatedRoute#snapshot](https://angular.kr/api/router/ActivatedRoute#snapshot)

<br/>
<br/>


## ActivatedRoute Class
- 아웃렛에 로드된 구성 요소와 연결된 경로에 대한 정보에 대한 액세스를 제공합니다. 이 명령을 사용하여 라우터 상태 트리를 이동하고 노드에서 정보를 추출합니다.

<br/>

### 속성들
|Property|return Type|Descripton|
|--------|-----------|----------|
|snapshot|ActivatedRouteSnapshot|이 경로의 현재 스냅샷|
|url|Observable\<UrlSegment\[ ]>|이 경로와 일치하는 URL 세그먼트의 관찰 가능 항목입니다.|
|params|Observable\<Params>|이 경로로 범위가 지정된 행렬 매개변수의 관찰 가능 항목입니다.|
|queryParams|Observable\<Params>|모든 경로가 공유하는 쿼리 매개변수의 관찰 가능 항목입니다.|
|fragment|Observable\<string \| null\>|모든 경로에서 공유하는 URL 조각의 관찰 가능 항목입니다.|
|data|Observable\<Data>|이 경로의 정적 및 확인된 데이터의 관찰 가능 항목입니다.|
|outlet|string|경로의 outlet 이름, 상수입니다.|
|compoent|Type\<any> \| string \| null|경로의 구성 요소, 상수입니다.|
|routeConfig|Route \| null|이 경로를 일치시키는 데 사용되는 구성입니다.|
|root|ActivatedRoute|라우터 상태의 루트입니다.|
|parent|ActivatedRoute \| null|라우터 상태 트리에서 이 경로의 부모입니다.|
|firstChild|ActivatedRoute \| null|라우터 상태 트리에서 이 경로의 첫 번째 자식입니다.|
|childern|ActivatedRoute\[ ]|라우터 상태 트리에서 이 경로의 자식입니다.|
|pathFromRoot|ActivatedRoute\[ ]|라우터 상태 트리의 루트에서 이 경로까지의 경로입니다.|
|paramMap|Observable\<ParamMap>|경로에 특정한 필수 및 선택적 매개변수의 맵을 포함하는 Observable입니다. 맵은 동일한 매개변수에서 단일 및 다중 값 검색을 지원합니다.|
|queryParamMap|Observable\<ParamMap>|모든 경로에 사용할 수 있는 쿼리 매개변수의 맵을 포함하는 Observable입니다. 맵은 쿼리 매개변수에서 단일 및 다중 값 검색을 지원합니다.|


<br/>
<br/>

## 	ActivatedRouteSnapshot Class
- 특정 시점에 outlet에 로드된 구성 요소와 연결된 경로에 대한 정보를 포함합니다. ActivatedRouteSnapshot을 사용하여 라우터 상태 트리를 탐색할 수도 있습니다.

### 속성들

|Property|return Type|Descripton|
|--------|-----------|----------|
|routeConfig|Route\| null|이 경로와 일치하는 데 사용되는 구성 *|
|url|UrlSegment\[ ]|이 경로와 일치하는 URL 세그먼트|
|params|Params|이 경로로 범위가 지정된 행렬 매개변수입니다.|
|**queryParams**|**Params**|**모든 경로에서 공유하는 쿼리 매개변수 value**|
|fragment|string \| null |모든 경로가 공유하는 URL 조각|
|data|Data|이 경로의 정적 및 확인된 데이터|
|outlet|string|경로의 outlet 이름|
|component|Type\<any>\|string\|null|경로의 구성 요소|
|root|ActivatedRouteSnapshot|라우터 상태의 루트|
|parent|ActivateRouteSnapshot\|null|라우터 상태 트리에서 이 경로의 부모|
|firstChild|ActivatedRouteSnapshot \| null |라우터 상태 트리에서 이 경로의 첫 번째 자식|
|children|ActivatedRouteSnapShot\[ ]|라우터 상태 트리에서 이 경로의 자식|
|pathFromRoot|ActivatedRouteSnapshot\[ ]|라우터 상태 트리의 루트에서 이 경로까지의 경로|
|paramMap|ParamMap|Read-Only|
|queryParamMap|ParamMap|Read-Only|

<br/>
<br/>

### Params 자료형
```typescript
type Params = {
    [key: string]: any;
};
```