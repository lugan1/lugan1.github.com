---
title: "[angular] Component 간에 페이지 이동하기 (router)"
tags:
- log
- angular
- typescript
categories:
- angular
date: '2021-10-06 14:41:00'
classes: wide
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




