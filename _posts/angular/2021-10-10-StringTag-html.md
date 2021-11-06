---
title: "[angular] String변수에 태그들 HTML에 적용방법"
tags:
- log
- angular
categories:
- angular
date: '2021-10-10 19:40:00'
classes: wide
---


# String 변수에 태그들을 HTML에 적용하는 방법
- bind-innerHTML="변수명" 을 사용한다

예제)

```html
<div class="content" bind-innerHTML='content'></div>
```

