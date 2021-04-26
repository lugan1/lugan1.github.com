---
title: "[Blog] 포스트 제목에 하이퍼링크 밑줄 없애는 방법"
classes : wide
tags:
- minimal_mistakes
- scss
- github pages
categories:
- Blog
---

홈 화면과 포스트 리스트에서 제목에 하이퍼링크 밑줄이 생기는게 약간 거슬려서 하이퍼링크 밑줄을 없앨수 있는 방법 어디 없나 하고 찾아보았다.

<https://devinlife.com/howto%20github%20pages/github-pages-settings/>

devinlife님의 블로그를 참조하여 밑줄 없애는 방법을 찾았다.



다음과 같은 경로에서 base.scss 파일을 수정하면 된다.


**sass -> minimal_mistakes -> base.scss**




![](/assets/image/posts_image/hyperlink_undline.png)
**links 항목에 text-decoration : none; 한줄을 추가하면 포스트제목에 하이퍼링크 밑줄이 없어진다.**
