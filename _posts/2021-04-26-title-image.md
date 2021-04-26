---
title: "[Blog] 상단의 타이틀 이미지 넣는방법"
tags:
- github pages
- minimal_mistakes
- scss
- html
categories:
- Blog
date: '2021-04-26 10:13:27 +0900'
classes: wide
last_modified_at: '2021-04-26 11:15:05 +0900'
---

상단의 타이틀 이미지 넣는법
--------

step 1. 먼저 높이 365px의 길이인 이미지를 준비한다. (그냥 웰페이퍼 이미지 아무거나 가져와서 365px 만큼의 높이로 자르기한다.)
<br>
step 2. 다음과 같은 파일을 수정한다. \_includes/mastehead.html
<br>
step 3. 맨 아랫줄에 다음과 같은 코드를 삽입한다. 저장한다.
<br>
<br>
```html
<div class="title_image">
  <nav id="site-nav" class="splash-nav">
    <div class="t_img"><img src="/assets/image/splash.png"></div>
    <div class="t_text">
      <p>타이틀 이미지에 넣을 텍스트</p>
    </div>
  </nav>
</div>
```
<br>
step 4. \_sass/minimal_mistakes/ 폴더에 css 파일을 하나 만든다. ex) \_titleImage.scss
<br>
step 5. 다음과 같은 코드를 삽입한다.
<br>
```css
.title_image {
	width: 100%;
    height: 350px;
	border-top: 1px solid rgba(255, 255, 255, 0.6);
    border-bottom: 1px solid rgba(255, 255, 255, 0.6);
	position: relative;
}
.t_img {
	width: 100%;
    height: 350px;
	vertical-align: middle;
}
.t_text {
    font-size: 50px;
    color: #ffffff;
    text-shadow:
    -1px -1px 0 #000,
    1px -1px 0 #000,
    -1px 1px 0 #000,
    1px 1px 0 #000;  
	text-align: center;
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate( -50%, -50% );
}
```

각 속성값은 알아서 커스터마이징 한다.
<br>
step 6. \_sass/minimal_mistakes.scss 를 수정한다. 다음과 같은 코드를 삽입한다.
<br>

![code](/assets/image/posts_image/post_titleImage/minimal.png)

```css
@import "minimal-mistakes/titleImage";
```
<br>
<br>
step 7. 타이틀 이미지 예시)
<br>
![code](/assets/image/posts_image/post_titleImage/example.png)
<br>
<br>
