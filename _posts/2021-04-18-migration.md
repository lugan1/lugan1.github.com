---
title: "[github pages] 구글 블로그 에서 깃허브 블로그로 이전하는 방법 (1)"
categories:
- github pages
tags:
- blogger
- github pages
- migration
- jekyll
- ruby
- jekyll_import
---

이제 깃허브 블로그 생성, 포스트글 올리는 법을 알았으니 구글 블로그에 있는 포스트 들을 깃허브 블로그로 이전 시켜야 된다.

구글링으로 방법을 찾아보니 친절하게 나와있다. 다음과 같은 블로그와 사이트들을 참고했다.

#### hahwul 님의 블로그  
##### <https://www.hahwul.com/2020/08/01/blogger-to-github-page/>

#### import jekyll 홈페이지 
#### <https://import.jekyllrb.com/docs/blogger/>
jekyll-import 홈페이지에 사용방법, 설치 방법들이 자세히 나와있다.


jekyll-import 는 다양한 블로그들의 백업본 파일을, 게시글별로 각각 파싱해주어서 jekyll형식의 post 파일로 변경해주는 라이브러리같다.

언어는 ruby를 사용한다. 따라서 ruby가 없으면 ruby를 설치해 주어야 한다.


지원해주는 블로그들은 다음과 같다.

* Behance
* Blogger (내가 사용했던 구글 블로그)
* CSV
* Dotclear
* Drupal 6
* Drupal 7
* EasyBlog
* Enki
* Ghost
* Google Reader
* Joomla
* Joomla 3
* Jrnl
* Marley
* Mephisto
* Movable Type
* PluXML
* Posterous
* Roller
* RSS
* S9Y
* S9Y Database
* Textpattern
* Third-party
* Tumblr
* Typo
* WordPress
* WordPress.com






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

---

### 2014-04-20 업데이트.

cmd 에서 명령어 실행안되서 보았더니

bash 에서 실행해야 되는 거였다.

<https://sanghaklee.tistory.com/39>

따라서 bash 설치

설정 -> 업데이트 및 복구 -> 개발자용

에서 개발자모드 on

설정 -> 검색 -> windows 기능에서 linux용 windows 하위 시스템(베타) 체크 및 재부팅


cmd 에서 lxrun/ install 하려그러는데 설치가 잘안되서


윈도우 앱스토어에서 ubunt 설치.

ubunt 실행후, 새 계정 이름과 비밀번호를 입력후 진행하고

창을 닫고

cmd 창에서 bash 입력하면 bash 창으로 변하는것 확인가능



하지만 ruby 명령어를 실행하려니까 cmd 창에서는 ruby -v 가 되던게

bash 에서는 ruby 가 설치 안되어있다고 나와서 ruby를 설치해야됨.

<https://smartbase.tistory.com/44>

를 따라서 ruby를 설치한다.


`sudo apt-get update`


# rbenv 설치하기 
<div class="colorscripter-code" style="color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#272727;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">git&nbsp;clone&nbsp;https:<span style="color:#0086b3"></span><span style="color:#ff3399">/</span><span style="color:#0086b3"></span><span style="color:#ff3399">/</span>github.com<span style="color:#0086b3"></span><span style="color:#ff3399">/</span>rbenv<span style="color:#0086b3"></span><span style="color:#ff3399">/</span>rbenv.git&nbsp;~<span style="color:#0086b3"></span><span style="color:#ff3399">/</span>.rbenv&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#4be6fa">echo</span>&nbsp;<span style="color:#ffd500">'export&nbsp;PATH="$HOME/.rbenv/bin:$PATH"'</span>&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">&gt;</span><span style="color:#0086b3"></span><span style="color:#ff3399">&gt;</span>&nbsp;~<span style="color:#0086b3"></span><span style="color:#ff3399">/</span>.bashrc&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#4be6fa">echo</span>&nbsp;<span style="color:#ffd500">'eval&nbsp;"$(rbenv&nbsp;init&nbsp;-)"'</span>&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">&gt;</span><span style="color:#0086b3"></span><span style="color:#ff3399">&gt;</span>&nbsp;~<span style="color:#0086b3"></span><span style="color:#ff3399">/</span>.bashrc&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#4be6fa">exec</span>&nbsp;$SHELL</div></div><div style="text-align:right;margin-top:-13px;margin-right:5px;font-size:9px;font-style:italic"><a href="http://colorscripter.com/info#e" target="_blank" style="color:#4f4f4ftext-decoration:none">Colored by Color Scripter</a></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#4f4f4f;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>

각각 한줄식 실행한다.


# ruby-build 설치하기 
<div class="colorscripter-code" style="color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#272727;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">git&nbsp;clone&nbsp;https:<span style="color:#0086b3"></span><span style="color:#ff3399">/</span><span style="color:#0086b3"></span><span style="color:#ff3399">/</span>github.com<span style="color:#0086b3"></span><span style="color:#ff3399">/</span>rbenv<span style="color:#0086b3"></span><span style="color:#ff3399">/</span>ruby<span style="color:#0086b3"></span><span style="color:#ff3399">-</span>build.git&nbsp;~<span style="color:#0086b3"></span><span style="color:#ff3399">/</span>.rbenv<span style="color:#0086b3"></span><span style="color:#ff3399">/</span>plugins<span style="color:#0086b3"></span><span style="color:#ff3399">/</span>ruby<span style="color:#0086b3"></span><span style="color:#ff3399">-</span>build&nbsp;</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#4be6fa">echo</span>&nbsp;<span style="color:#ffd500">'export&nbsp;PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"'</span>&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">&gt;</span><span style="color:#0086b3"></span><span style="color:#ff3399">&gt;</span>&nbsp;~<span style="color:#0086b3"></span><span style="color:#ff3399">/</span>.bashrc</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#4be6fa">exec</span>&nbsp;$SHELL</div></div><div style="text-align:right;margin-top:-13px;margin-right:5px;font-size:9px;font-style:italic"><a href="http://colorscripter.com/info#e" target="_blank" style="color:#4f4f4ftext-decoration:none">Colored by Color Scripter</a></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#4f4f4f;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>




configure: error: no acceptable C compiler found in $PATH
에러시 해결방법

<https://itknowledge.tistory.com/12>

C컴파일러가 없어서 발생하는 에러라고 한다.

다음 명령어 실행

`sudo apt-get install build-essential`


루비 설치방법
`sudo apt-get install ruby-full`

설치가 완료되었다면
`ruby -v`
명령어를 실행해서 버전을 확인하자.
버전이 제대로 표시된다면 설치 성공.

bundler 도 같이 설치하자.

bundler : gem 의 의존성 관리를 위해 사용하는 의존성 관리도구.
gem : ruby에서 사용하는 패키지

다음 명령어를 입력해서 bundler를 설치.
`gem install bundler`


<br>
### You don't have write permissions for the /var/lib/gems/2.7.0 directory
### 에러 뜰시 해결방법

<https://int-i.github.io/linux/2020-09-07/ruby-no-permission/>

아래와 같이 환경변수를 추가한다.

<div class="colorscripter-code" style="color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#272727;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#4be6fa">echo</span>&nbsp;<span style="color:#ffd500">'#&nbsp;Install&nbsp;Ruby&nbsp;Gems&nbsp;to&nbsp;~/gems'</span>&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">&gt;</span><span style="color:#0086b3"></span><span style="color:#ff3399">&gt;</span>&nbsp;~<span style="color:#0086b3"></span><span style="color:#ff3399">/</span>.bashrc</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#4be6fa">echo</span>&nbsp;<span style="color:#ffd500">'export&nbsp;GEM_HOME="$HOME/gems"'</span>&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">&gt;</span><span style="color:#0086b3"></span><span style="color:#ff3399">&gt;</span>&nbsp;~<span style="color:#0086b3"></span><span style="color:#ff3399">/</span>.bashrc</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#4be6fa">echo</span>&nbsp;<span style="color:#ffd500">'export&nbsp;PATH="$HOME/gems/bin:$PATH"'</span>&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">&gt;</span><span style="color:#0086b3"></span><span style="color:#ff3399">&gt;</span>&nbsp;~<span style="color:#0086b3"></span><span style="color:#ff3399">/</span>.bashrc</div><div style="padding:0 6px; white-space:pre; line-height:130%">source&nbsp;~<span style="color:#0086b3"></span><span style="color:#ff3399">/</span>.bashrc</div></div><div style="text-align:right;margin-top:-13px;margin-right:5px;font-size:9px;font-style:italic"><a href="http://colorscripter.com/info#e" target="_blank" style="color:#4f4f4ftext-decoration:none">Colored by Color Scripter</a></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#4f4f4f;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>

다시 bundler 설치명령어를 실행해 bundler를 설치한다.

<div class="colorscripter-code" style="color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#272727;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">gem&nbsp;install&nbsp;bundler</div><div style="padding:0 6px; white-space:pre; line-height:130%">gem&nbsp;update</div><div style="padding:0 6px; white-space:pre; line-height:130%">gem&nbsp;install&nbsp;jekyll&nbsp;bundler</div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#4f4f4f;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>

이제 <https://import.jekyllrb.com/docs/installation/> 에서 나온대로

`gem install jekyll-import`

명령어를 실행해서 지킬임포트 를 설치한다.


이제 bash 에서 루비도 설치되었고, gem 도 설치되었고 jekyll-import 도 설치되었다.

다시 처음으로 돌아가서 구글 백업 xml 을 파싱해보자.

cd 명령어로 구글 백업.xml 파일이 있는곳으로 이동한다.

그리고 다음 명령어를 실행한다.


<div class="colorscripter-code" style="color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#272727;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">ruby&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">-</span>r&nbsp;rubygems&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">-</span>e&nbsp;\'require&nbsp;<span style="color:#ffd500">"jekyll-import"</span>;</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;JekyllImport::Importers::Blogger.run({</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#ffd500">"source"</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span><span style="color:#0086b3"></span><span style="color:#ff3399">&gt;</span>&nbsp;<span style="color:#ffd500">"백업본.xml"</span>,</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#ffd500">"no-blogger-info"</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span><span style="color:#0086b3"></span><span style="color:#ff3399">&gt;</span>&nbsp;<span style="color:#c10aff">false</span>,&nbsp;<span style="color:#999999">#&nbsp;not&nbsp;to&nbsp;leave&nbsp;blogger-URL&nbsp;info&nbsp;(id&nbsp;and&nbsp;old&nbsp;URL)&nbsp;in&nbsp;the&nbsp;front&nbsp;matter</span></div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#ffd500">"replace-internal-link"</span>&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span><span style="color:#0086b3"></span><span style="color:#ff3399">&gt;</span>&nbsp;<span style="color:#c10aff">false</span>,&nbsp;<span style="color:#999999">#&nbsp;replace&nbsp;internal&nbsp;links&nbsp;using&nbsp;the&nbsp;post_url&nbsp;liquid&nbsp;tag.</span></div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;})\'</div></div><div style="text-align:right;margin-top:-13px;margin-right:5px;font-size:9px;font-style:italic"><a href="http://colorscripter.com/info#e" target="_blank" style="color:#4f4f4ftext-decoration:none">Colored by Color Scripter</a></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#4f4f4f;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>



source 항목에 값만 바꾸어주면된다. 구글백업.xml 이 있는 경로로 바꾼다.

메모장 같은데다가 옮기고 source 값만 바꾸고 통째로 복사 붙여넣기 해서 bash 에서 실행한다.





### jekyll-import-0.20.0/lib/jekyll-import/importers/blogger.rb:189:in \`tag_end': undefined method \`decode' for URI:Module (NoMethodError)

### 에러 뜰시에 해결방법.



jekyll-import-0.20.0 /lib/jekyll-import/importers/blogger.rb:189:in\`tag_end': URI : Module에 대한 정의되지 않은 메소드\`decode' (NoMethodError)


C:\Users\[user 이름]\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_\[설치된 우분투]\LocalState\rootfs\home\우분투 계정\gems\gems\jekyll-import-0.20.0\lib\jekyll-import\importers\blogger.rb

에서 에러가 나온다는말.


말그대로 URI Module 에서 decode 메소드가 정의되지 않았다는 뜻이다. VScode 로 해당 라인, 해당 파일 열어보니 URI.decode(\~\~\~) 라인에서 에러가 걸린다.

일단 루비 문법을 하나도 몰라서 아주 기초적인 루비 문법을 공부했다.

루비는 보통 def~~ 로 시작하면 end 로 끝나는거 같고, 변수선언시 자료형은 따로 안적어주는것 같다.

모듈이라고 불리는 것은, 다른 외부 파일에서 메소드를 쓸수 있게 해주는것같다.

require "파일경로"

로 다른 파일을 불러와서 사용한다. 자바의 import 랑 비슷한 개념인것 같다.

루비의 출력은 print("\~~") 로 하는데 디버그시에 유용히 쓰여질거같다.

<https://rubyapi.org/3.0/o/s?q=uri>

사이트에서 URI 메소드에는 어떤것이 들어있나 찾아보았더니 decode 메소드는 없었다.

대신 URI.decode_www_form (String) 메소드가 있었다.

Example

<div class="colorscripter-code" style="color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important;overflow:auto"><table class="colorscripter-code-table" style="margin:0;padding:0;border:none;background-color:#272727;border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px 0;text-align:left"><div style="margin:0;padding:0;color:#f0f0f0;font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important;line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">ary&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span>&nbsp;URI.decode_www_form(<span style="color:#ffd500">"a=1&amp;a=2&amp;b=3"</span>)</div><div style="padding:0 6px; white-space:pre; line-height:130%">ary&nbsp;&nbsp;&nbsp;<span style="color:#999999">#=&gt;&nbsp;\[\['a',&nbsp;'1'],&nbsp;\['a',&nbsp;'2'],&nbsp;\['b',&nbsp;'3']]</span></div></div></td><td style="vertical-align:bottom;padding:0 2px 4px 0"><a href="http://colorscripter.com/info#e" target="_blank" style="text-decoration:none;color:white"><span style="font-size:9px;word-break:normal;background-color:#4f4f4f;color:white;border-radius:10px;padding:1px">cs</span></a></td></tr></table></div>

예제를 보니, Key-value 배열로 리턴해 주는 메소드인것 같다.


바로 blogger.rb 파일내의

file_name = URI.decode("#{post_data\[:filename]}.html") 를 주석처리하고

file_name = URI.decode_www_form("#{post_data\[:filename]}.html")

를 새로 기입했다. (VScode 로 작업했다.)

URI.decode_www.form() 메소드는 

C:\Users\유저이름\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_설치된 우분투\LocalState\rootfs\home\우분투 계정\gems\gems\uri-0.10.1\lib\uri\common.rb

에 들어있었다.

하고 실행시키니

URI.decode~~ 밑줄인 

file.open (\~\~~file_name) 라인 에서 EISDIR 에러가 뜨는 거였다.

print로 file_name 을 찍어보니 key_value 형식으로 나오긴 하는데 \[\~\~~.html, ""] 형식으로 value가 공백으로 나오는거였다.

뭔가 생각해보니 file_name이 key_value 형식으로 나오면 안될꺼같아서

URI.decode_www_form_component 로 바꾸니까 해결되었다.


![solution.png](/assets/image/posts_image/post_moved/solution.png)

file_name 을 print 로 찍어보니까 key value 맵 형식이 아닌, 말그대로 html 파일이름이 찍혔다. 아마 key_value의 map형식 배열을 file.open 메소드에 넣으니 오류가 난것같다.

![filename](/assets/image/posts_image/post_moved/filename.png)

실행이 완료되었으면

\_posts 폴더가 생성될것이고 그안에

구글 블로그 포스트들 html 파일들이 생성되어있다.


![postpath.png](/assets/image/posts_image/post_moved/postpath.png)

![posts.png](/assets/image/posts_image/post_moved/posts.png)

뭔가 감이온다. 이거를 현재 사용중인 깃 블로그의 repository의 \_posts 폴더로 옮기면 될것같다.

옮긴다음 locallhost:4000 을 돌려보았는데. 바로 warning 메세지가 떳다.

![warning.png](/assets/image/posts_image/post_moved/warning.png)


게시글들은 올라왔는지 들어가 확인했는데 레이아웃이 표시가 안되고 빈페이지에 글과 사진들과 html 태그들이 표시되고 있다.

아까 wrning 메세지가 뜬것이 생각난다.

빌드 경고 : _posts / 2021-04-17-git-blog.html 에서 요청한 레이아웃 'post'가 존재하지 않습니다.

이뜻인거 같은데 바로 파일을 열어보았다. (VScode 로 작업했다.)

![layout_ploblem.png](/assets/image/posts_image/post_moved/layout_ploblem.png)

layout : post 이부분이 문제인거 같다. Single 로 변경해주어야 한다. 혹은 아예 지워서 공백으로 만들던지 해야된다.

author : 항목도 지워야지 왼쪽 사이드에 프로필이 표시되어서 나온다. (minimanl_mistakes 테마인경우)

categories : 항목도 없어서 새로 추가해줘야 한다.

포스트가 몇개 안되면 수작업으로 파일들 일일히 열어서 수정할수 있겠지만

포스트가 몇백개 이상되면 상당한 노가다가 요구될거 같다.


따로 c 든 java든 python 이든 써서 일괄적으로 폴더내의 파일을 열고 파일내용을 바꾸고 저장하는 코드를 작성해야 될거같다.
