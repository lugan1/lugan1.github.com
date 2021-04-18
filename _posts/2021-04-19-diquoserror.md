---
title: disquos 덧글 기능 추가시 We were unable to load Disqus 오류 해결방법
categories:
- github pages
tags:
- markdown
- md
- disquos
---

disquos 회원가입을 하고, config.yml 에 추가하고 short name 까지 추가했는데, 포스트 덧글란에 We were unable to load Disqus 라고 메세지가 뜨면서 덧글기능이 추가가 안되어 있었다.

찾아보니 **disquos 설정에서 신뢰된 사이트에 내 사이트가 등록이 안되어서** 그런것이었다.


**Disquos 설정 -> advanced -> trusted Domains** 에 내 사이트 주소를 입력해서 해결.
