---
title: "[Blog] 깃허브 페이지가 업데이트 안되던 issue"
classes : wide
tags:
- github pages
- error
categories:
- Blog
date: '2021-10-11 06:31:00'
---

# 깃허브 페이지가, 포스트 commit push 를 해도 업데이트 되지 않았던 issue
- 리포지토리 settings -> pages 에 보면 제대로 빌드가 되었는지 확인할 수 있다.

<br/>

![pages_build_fail.png](/assets\image\posts_image\pages_build_fail.png)

<br/>

## 빌드 실패에 대한 자세한 내용은 표시되지 않는데, 로컬에서 빌드 돌려보면 실패 내용을 알 수 있다.
- cmd 창을 열고, 프로젝트 폴더에서 bundle exec jekyll serve 실행한다.

<br/>
<br/>

## 내 경우에는 앵귤러 데이터 바인딩에서 \{\{ 변수명 \}\} 이라고 내용을 적어서 포스팅 했던게 빌드하는데 오류가 났었다.
- Mat Table 포스트에서 `\``html \{\{ 변수명 \}\} \``` 쓰는것도 빌드 오류에 걸렸다. 중괄호{ } 변수명을 포스트내용에 쓸때 주의를 해야겠다. 이스케이프 문자 \\ 를 적절히 활용해서 써야한다.



