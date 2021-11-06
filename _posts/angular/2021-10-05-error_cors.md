---
title: "[angular] has been blocked by CORS policy: Cross origin requests are only supported for protocol "
tags:
- log
- angular
- error
categories:
- angular
date: '2021-10-05 15:54:00'
classes: wide
---

# 출저 및 참고 사이트 :  
[https://devchul.tistory.com/6](https://devchul.tistory.com/6)  
<br/>

[https://javaengine.tistory.com/entry/Spring-Rest-api-Angular-framework%EB%A1%9C-%EC%9B%B9%EC%82%AC%EC%9D%B4%ED%8A%B8-%EB%A7%8C%EB%93%A4%EA%B8%B02-%E2%80%93-%EB%A1%9C%EA%B7%B8%EC%9D%B8%EA%B0%80%EC%9E%85HttpClient-Proxy-Validation](https://javaengine.tistory.com/entry/Spring-Rest-api-Angular-framework%EB%A1%9C-%EC%9B%B9%EC%82%AC%EC%9D%B4%ED%8A%B8-%EB%A7%8C%EB%93%A4%EA%B8%B02-%E2%80%93-%EB%A1%9C%EA%B7%B8%EC%9D%B8%EA%B0%80%EC%9E%85HttpClient-Proxy-Validation)


# Angular로 작성한 front 에서 백엔드 서버의 HTTP GET API 호출시에 has been blocked by CORS policy: Cross origin requests are only supported for protocol
- CORS : Cross-Origin Resource Sharing (교차 출저 리소스 공유)
- angular와 같은 Front web 프레임워크로 웹사이트를 구축할때는 외부 리소스를 사용하기 위해 api 서버와 통신이 필요하다. 그런데 브라우저에서 ajax를 이용하여 외부 리소스를 호출할때 현재 도메인내에서 다른 도메인의 주소(port도 구별)를 호출하면 크로스 도메인이라고 하여 브라우저에서 보안 오류를 내며 통신이 실패한다. 따라서 localhost:4200에서 localhost:8080으로의 호출은 현재로선 불가능하다.

- 이를 처리하기 위해서는 api 서버의 설정을 바꾸어 crossdomain 처리가 가능하게 하는 방법과 Proxy를 이용하여 클라이언트에서 처리하는 방법 2가지가 있다. api의 설정을 바꿔 어떤 클라이언트든 받아들이는것은 좋지 않은 방법이라 생각되므로 두번째 방법인 Proxy를 이용하여 처리한다.

- 다행히도 angular에서는 Proxy설정을 기본으로 지원하고 있다. api주소를 현재도메인(localhost:4200)으로 호출하더라도 내부적으로 localhost:8080으로 리소스를 요청해주는 기능이다.

<br/>

# 해결방법
- 프로젝트 root 에서 proxy.conf.json 파일을 생성한다.
- proxy.conf.json 파일을 다음과 같이 작성한다.


**proxy.conf.json 파일**
```
{
  "/api/*" : {
    "target" : "http://localhost:8087",
    "secure" : false,
    "logLevel" : "debug",
    "pathRewrite": {
      "^/api": ""
    }
  }
}
```
- package.json 파일을 열어서 start : 항목에 다음과 같이 수정한다.
- 즉 서버를 실행할때 다음과 같은 명령어를 자동으로 실행하게 된다.

```ng serve --proxy-config proxy.conf.json```

- 이렇게 할시에 api 호출시에는 /api/ 가 접두사에 붙는다.
- 만약 백엔드 서버의 api 호출 url 이 api/back/board/getAllPost 이면, Fornt 어플리케이션에서 /api/api/back/board/getAllPost 로 호출해야 된다.


