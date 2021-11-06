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
last_modified_at: '2021-04-27 11:44:47 +0900'
---

#### 이미지 사이즈 맞추는법 object fit    <https://nykim.work/86>

#### 이미지 가운데 정렬, 동적 사이즈 조절 <https://webdir.tistory.com/487>

사이트를 참고했다.

<br>
<br>
step 1. 먼저 너비 1520, 높이 1140 정도의 4:3 비율의 이미지를 준비한다. (그냥 웰페이퍼 이미지 아무거나 가져와서 4:3비율만큼 자르기한다.)<br>
<br>
step 2. 다음과 같은 파일을 수정한다. \_includes/mastehead.html
<br>
(만약 홈화면에서만 타이틀 이미지 뜨게하고, 포스트글에서는 안뜨게 하려면 \_mastehead.html 말고, \_layout 폴더에 archive.html  파일을 수정하면 된다.)
<br>
....<br>
include page__hero_video.html <br>
...<br>
end if<br>

밑에다가 아래의 코드 삽입하면 된다.

<br>
<br>
step 3. 맨 아랫줄에 다음과 같은 코드를 삽입한다. 저장한다.
<br>
<br>
```html
<div class="title_image">
    <div class="t_img">
      <img src="/assets/image/이미지 경로">
    </div>

    <div class="t_text">
      <p>타이틀 이미지에 넣을 텍스트</p>
    </div>
</div>
```
<br>
step 4. \_sass/minimal_mistakes/ 폴더에 css 파일을 하나 만든다. ex) \_titleImage.scss
<br>
step 5. 다음과 같은 코드를 삽입한다.
<br>
```css
.title_image {
    max-width: 100%;
    height: 380px;      //height 380 일시에 너비 1520, 높이 1140 정도의 4:3 비율의 이미지 필요
    border-top: 1px solid rgba(255, 255, 255, 0.6);
    border-bottom: 1px solid rgba(255, 255, 255, 0.6);
    position:relative;
    overflow:hidden;                //넘치는 부분은 자름
}
.t_img {
    object-fit: cover;
    width: 100%;
    position:absolute;
    top:0;
    left: 0;
    right: 0;
    bottom: 0;
    -webkit-transform: translate(50%,50%); 
    -ms-transform: translate(50%,50%); 
    transform: translate(50%,50%);
}

.title_image .t_img img{
    object-fit: cover;
    position: absolute; 
    top: 0; 
    left: 0;
    max-width: 100%; 
    height: auto; 
    -webkit-transform: translate(-50%,-50%); 
    -ms-transform: translate(-50%,-50%); 
    transform: translate(-50%,-50%);
}

.t_text {
    width: auto;
    height: auto;
    font-size: 50px;
    font-weight: bold;
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
	transform: translate( -50%, -50% ); //위치이동, 왼쪽 50%이동, 위쪽 50%이동, -는 왼쪽, +는 오른쪽, -는 위쪽 +는 밑에쪽
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
