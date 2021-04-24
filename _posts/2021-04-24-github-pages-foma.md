---
title: "[github pages] 포스트글에 표기되는 date 포맷 변경하는 방법"
tags:
- github pages
- minimal_mistakes
categories:
- github pages
date: '2021-04-24 21:12:20 +0900'
last_modified_at: '2021-04-25 01:36:26 +0900'
---

사이트에 영문으로 날짜표기되는게 마음에 안들어서 한글로 표기되도록 date 포맷을 변경했다.

다음과 같은 경로의 파일을 수정한다. (텍스트 에디터로 수정하면 된다. 나는 VScode로 수정했다.)



업데이트 날짜 표기관련 포맷

\lugan1.github.io\_includes\page_date.html

![date](/assets/image/posts_image/jekyll_admin_date/page_dateHTML.png)


최근 업데이트 날짜 없을시에 업데이트 표기가 안뜨게 할려면 다음과 같은 코드를 지운다. 업데이트 없을시에 기본날짜로 표기되게 하고싶으면 코드를 남긴다.




게시글 상단의 날짜 표기관련 포맷


\lugan1.github.io\_includes\page_meta.html

![meta](/assets/image/posts_image/jekyll_admin_date/page_metaHTML.png)



날짜 포맷 관련은 여기서 참고했다.

<https://blog.yena.io/studynote/2017/11/06/Date-Formatting.html>
