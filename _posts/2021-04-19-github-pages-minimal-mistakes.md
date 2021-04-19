---
title: "[github pages] minimal_mistakes 파일구조"
tags:
- minimal_mistakes
- github pages
categories:
- github pages
---

<https://mmistakes.github.io/minimal-mistakes/docs/stylesheets/>

<br>
<br>
<br>
minmal_mistakes 폴더 경로

**[repository] -> \_sass -> minimal_mistakes**
<br>
<br>
<br>
<br>
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
<br>|     ├── _masthead.scss       # masthead
<br>|     ├── _mixins.scss         # mixins (em function, clearfix)
<br>|     ├── _navigation.scss  # nav links (breadcrumb, priority+, toc, pagination, etc.)
<br>|     ├── _notices.scss        # notices
<br>|     ├── _page.scss           # pages
<br>|     ├── _print.scss          # print styles
<br>|     ├── _reset.scss          # reset
<br>|     ├── _sidebar.scss        # sidebar
<br>|     ├── _syntax.scss         # syntax highlighting
<br>|     ├── _tables.scss         # tables
<br>|     ├── _utilities.scss      # utility classes (text/image alignment)
<br>|     └── _variables.scss      # theme defaults (fonts, colors, etc.)  
<br>├── assets
<br>|  ├── css
<br>|  |  └── main.scss            # main stylesheet, loads SCSS partials in _sass
