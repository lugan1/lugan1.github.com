---
title: "[github pages] 구글 블로그 에서 깃허브 블로그로 이전하는 방법"
categories:
- github pages
tags:
- blogger
- github pages
- migration
- jekyll
---

이제 깃허브 블로그 생성, 포스트글 올리는 법을 알았으니 구글 블로그에 있는 포스트 들을 깃허브 블로그로 이전 시켜야 된다.

구글링으로 방법을 찾아보니 친절하게 나와있다. 다음과 같은 블로그와 사이트들을 참고했다.

<https://www.hahwul.com/2020/08/01/blogger-to-github-page/>

<https://import.jekyllrb.com/docs/blogger/>


일단 구글 블로그에서 컨텐츠 백업을 해야된다.

설정 항목 -> 블로그 관리 -> 콘텐츠 백업
을 누르면 백업본 xml 파일이 다운될것이다.


Vscode로 열어보면 다음과 같이 쭉 나열되어있다.

![백업본내용](/assets/image/posts_image/backup_xml.png)


이제 이 내용들을 전부다 파싱 해주어서 각각의 html 파일들로 만들어 줘야 한다.

jekyll import를 이용하면 각각의 내용들을 파싱해주어서 html 파일들로 만들수 있다고 한다.


cmd 창을 키고, repository 폴더로 이동한다음, 다음과 같은 명령어를 실행한다.

    gem install jekyll-import


Markdown 에서 명령어를 적다가 알게 된건데 스페이스바를 4번 누르면 CMD 명령어 형식으로 바뀌는것을 알았다.


jekyll-import 가 설치되었으면 다시 다음과 같은 명령어를 실행한다.


    ruby -r rubygems -e 'require "jekyll-import";
    JekyllImport::Importers::Blogger.run({
      "source"                => "./blog-08-01-2020.xml",
      "no-blogger-info"       => true, # not to leave blogger-URL info (id and old URL) in the front matter
      "replace-internal-link" => false, # replace internal links using the post_url liquid tag.
    })'
		
		
source 에는 아마도 백업본 경로를 적는것 같다.

코드를 보니 루비를 알아야 될것 같아서 루비를 공부한다.
