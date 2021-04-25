---
title: "[github pages] repository 폴더구조"
tags:
- minimal_mistakes
- github pages
categories:
- github pages
---

\_includes
<br>├── analytics-providers
 <br>|  └── custom.html
 <br>|  └── google.html
 <br>|  └── google-gtag.html
 <br>|  └── google-universal.html
<br>├── comments-providers                      #댓글 기능 제공 사이트 관련
 <br>|  └── custom.html
 <br>|  └── custom_scripts.html
 <br>|  └── discourse.html
 <br>|  └── disqus.html
 <br>|  └── facebook.html
 <br>|  └── scripts.html
 <br>|  └── staticman.html
 <br>|  └── staticman_v2.html
 <br>|  └── utterances.html
<br>├── footer
<br>|  └── custom.html
<br>├── head
<br>|  └── custom.html
<br>├── search
<br>|  └── algolia-search-scripts.html
<br>|  └── google-search-scritps.html
<br>|  └── lunar-search-scripts.html
<br>|  └── search_form.html
<br>├── analystics.html
<br>├── archive-single.html
<br>├── author-profile.html
<br>├── author-profile-custom-links.html
<br>├── breadcrumbs.html
<br>├── browser-upgrade.html
<br>├── category-list.html
<br>├── comment.html
<br>├── comments.html
<br>├── documents-collection.html
<br>├── feature_row
<br>├── footer.html
<br>├── gallery
<br>├── gruop-by-array
<br>├── head.html
<br>├── masthead.html
<br>├── nav_list
classes : wide
<br>├── page_date.html                         #post글들의 날짜 포맷설정. 
<br>├── page_hero.html
<br>├── page_hero_video.html
<br>├── page_meta.html
<br>├── page_taxonomy.html
<br>├── paginator.html
<br>├── post_pagination.html
<br>├── posts-category.html
<br>├── posts-tag.html
<br>├── posts-tag.html
<br>├── scripts.html
<br>├── seo.html
<br>├── sidebar.html
<br>├── skip-links.html
<br>├── social-share.html
<br>├── tag-list.html
<br>├── toc
<br>├── toc.html
<br>└── video
<br>

<br>
dataformat 관련 참고
yena님 블로그 : <https://blog.yena.io/studynote/2017/11/06/Date-Formatting.html>

<br>
<br>


<https://mmistakes.github.io/minimal-mistakes/docs/stylesheets/>

<br>
minmal_mistakes 폴더 경로

**[repository] -> \_sass -> minimal_mistakes**
<br>
<br>
minimal_mistakes 폴더 구조
<br>
 minimal-mistakes
<br>├── _sass
<br>|  └── minimal-mistakes
<br>|     ├── vendor               # vendor SCSS partials
<br>|     |   ├── breakpoint       # media query mixins
<br>|     |   ├── magnific-popup   # Magnific Popup lightbox
<br>|     |   └── susy             # Susy grid system
<br>|     ├── _animations.scss     # animations
<br>|     ├── _archive.scss        # archives (list, grid, feature views)
<br>|     ├── _base.scss           # base HTML elements 
<br>|     ├── _buttons.scss        # buttons
<br>|     ├── _footer.scss         # footer
<br>|     ├── _masthead.scss       # 상단 타이틀, 메뉴 레이아웃
<br>|     ├── _mixins.scss         # mixins (em function, clearfix)
<br>|     ├── _navigation.scss  # nav links (breadcrumb, priority+, toc, pagination, etc.)
<br>|     ├── _notices.scss        # notices
<br>|     ├── _page.scss           # 전체 페이지. 즉 전체 사이트 form 설정, 여기서 양옆 margin 설정가능
<br>|     ├── _print.scss          # print styles
<br>|     ├── _reset.scss          # reset
<br>|     ├── _sidebar.scss        # 양옆의 사이드바. 프로필부분
<br>|     ├── _syntax.scss         # syntax highlighting
<br>|     ├── _tables.scss         # tables
<br>|     ├── _utilities.scss      # utility classes (text/image alignment)
<br>|     └── _variables.scss      # theme defaults (fonts, colors, etc.)  
<br>├── assets
<br>|  ├── css
<br>|  |  └── main.scss            # main stylesheet, loads SCSS partials in _sass


<br>
<br>
\_site 폴더는 지워도 posts generating 시에 내용물과 함께 새로생김.

post의 날짜가 안적혀 있으면 파일의 이름 앞부분 yyyy-mm-dd 앞부분으로 날짜로 해서 post글을 생성함.
따라서 포스트글의 파일이름 날짜부분이 바뀌면 포스트글의 날짜도 바뀐다.
