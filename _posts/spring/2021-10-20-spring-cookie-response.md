---
title: "[spring] Cookie 로 응답하는 방법 "
tags:
- log
- spring
categories:
- spring
date: '2021-10-20 11:47:00'
classes: wide
---

# Spring Cookie 사용해서 Response 하기
- 로그인 할때 아이디 기억하기 체크박스를 클릭하면 쿠키를 받아와서 다음에 로그인 할때 아이디가 자동 입력되는 기능

<br/>
<br/>

# API 서버에서 쿠키가 있는지 검사하고, 쿠키가 있으면 쿠키값으로 로그인 하는 방법
- 컨트롤러의 API 매개변수에 @CookieValue 어노테이션을 추가한다.
- 컨트롤러에서 각 API Mapping 메소드에 @CookieValue(value="쿠키이름", required=필수여부false) Cookie 쿠키객체명 매개변수를 추가한다.
- 그럼 Cookie 객체를 받아와서 Cookie.getvalue 로 정보를 가져올 수 있다.


<br/>
<br/>

# API 서버에서 쿠키를 생성해서 응답하는 방법
- 만약 받은 Request에서 쿠키가 없으면 쿠키를 생성해서 돌려줘야 한다.

- Cookie cookie = new Cookie("쿠키이름", 저장할값) 으로 쿠키를 생성한다.

- cookie 가 생성되면 이름을 변경할 수 없다.


- cookie.setPath(클라이언트가 쿠키를 반환해야되는 쿠키 경로)

- cookie.setSecure(boolean)
  - 쿠키가 HTTPS 또는 SSL 과 같은 보안 프로토콜을 사용해서만 보내야 하는지 여부를 선택한다.
  - 기본값은 false다.

- cookie.setMaxAge(숫자) 로 유효기간을 설정한다.
  - 초단위로 설정된다.
  - 양수 값은 몇초가 지나면 쿠키가 만료됨을 나타낸다.
  - 음수 값은 쿠키가 영구적으로 저장되지 않고 웹 브라우저가 종료될때 삭제됨을 나타낸다. 0이면 쿠키가 삭제된다.


- cookie.setValue(String 문자열)
  - cookie 에 새 값을 할당한다.
  - 이진 값을 사용하는 경우 BASE64 인코딩을 사용할 수 있다.
  - 쿠키는 맵방식으로 되어있다
  - 문자를 &으로 끊고, = 으로 끊으면 데이터를 사용가능하다.
  - 보통은 파서가 알아서 해준다.


- API 받는 매개변수에 HttpServletResponse httpServletResponse를 추가한다.

- httpServletResponse.addCookie(cookie) 로 응답에 쿠키를 추가한다.

<br/>
<br/>
<br/>


**MVC 컨트롤러에서 쿠키생성 전체 코드**
```java
 @PostMapping("/login")
    public ResponseEntity Login(
            @RequestBody StudyLogin studyLogin,
            HttpSession httpSession,
            HttpServletResponse httpServletResponse,
            @CookieValue(value="REMEMBER", required = false)Cookie loginCookie){
        try{
            if(loginCookie != null){
                // 받은 쿠키가 있으면

                System.out.println("쿠키가 있음");
                System.out.println(loginCookie.getValue());
            }
            else if(loginCookie == null){
                // 받은 쿠키가 없으면
                System.out.println("쿠키가 없음. 쿠키 생성");

                if (studyLogin.isCookie() == true){
                    // front에서 쿠키 응답받기 checkBox를 체크 했으면 쿠키 생성

                    String cookie_value = "쿠키값_테스트";
                    cookie_value = URLEncoder.encode(cookie_value,"utf-8");
                    Cookie rememberCookie = new Cookie("REMEMBER", cookie_value);
                    rememberCookie.setPath("/api/back/user/login");
                    rememberCookie.setMaxAge(30);
                    httpServletResponse.addCookie(rememberCookie);
                }
            }
            StudytAuthIfno authInfo = studyAuthService.authenticate(studyLogin.getId(),studyLogin.getPassword());
            // loginCookie 가 null 이 아니면 loginCookie 에서 값을 가져와서 ID, Password 값을 넣는 식으로 변경해야됨

            httpSession.setAttribute("authInfo",authInfo);
            return new ResponseEntity("{ \"message\":\"login_success\"}", HttpStatus.OK);
        }catch (WrongPasswordException | UnsupportedEncodingException e){
            return new ResponseEntity("{ \"message\": \"login_failed\"}",HttpStatus.UNAUTHORIZED);
        }
    }
```


<br/>
<br/>

# 로그아웃시에 쿠키삭제 방법
- 로그아웃시에 쿠키의 유효시간을 0으로 지정하면 쿠키가 삭제된다.
- pornt 에서 response.addCookie(Cookies.createCookie("AUTH","","/", 0)); 을 작성한다.




# 클라이언트에서 ID 저장하기 쿠키 만드는 방법
```javascript
document.cookie = encodeURIComponent(name) + '=' + encodeURIComponent(value);
```
- 쿠키 만들시에 인코딩도 해야된다.