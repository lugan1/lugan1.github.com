---
title: "[error] IllegalArgumentException: An invalid character [32] was present in the Cookie value  "
tags:
- log
- error
- spring
categories:
- spring
date: '2021-10-20 15:49:00'
classes: wide
---

# IllegalArgumentException: An invalid character \[32] was present in the Cookie value
- 다음과 같은 문장에서 에러가 발생했다.
```java
httpServletResponse.addCookie(rememberCookie);
```
- 에러 내용은 쿠키에 invalid character \[32] 가 있다는 뜻이다.
- 해당 에러는 톰캣 8.5에서 새로 추가된 기본 쿠키 규칙 때문에 생긴것이다.
- 세미콜론, 콤마, 이콜 사인, 그리고 공백은 쿠키값으로 이용될 수 없다.

# 해결 방법
- 쿠키를 추가할때 UTF-8 로 인코딩을 먼저 해줘야 한다.

- httpServletResponse 에 쿠키를 추가하기 전에 다음과 같은 문장을 추가해준다.

```java
string cookie_Value = URLEncoder.encode(cookie_Value, "utf-8");
```

예제)
```java
String cookie_Value = "asdf";
string cookie_Value = URLEncoder.encode(cookie_Value, "utf-8");
httpServletResponse.addCookie(new Cookie("cookie_name",cookie_Value))
```
