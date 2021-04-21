---
title: "[github pages] 구글 블로그 에서 깃허브 블로그로 이전하는 방법 (2)"
---

저번에

#### [[github pages] 구글 블로그 에서 깃허브 블로그로 이전하는 방법 (2)](https://lugan1.github.io/github%20pages/migration/)

에서 구글 블로그 백업본.xml 파일을 루비 jekyll-import 라이브러리를 이용해 파싱해주어서 각각의 .html 파일로 생성하는데 까지 성공했다.



이번에는 각각의 게시글들 .html 파일을 내 홈페이지 양식에 맞게 변경해주어야 한다.


내가 생각한 방법은

C, java, pyhton 등을 이용해 File_open \-> 파일들의 문자열 수정 \-> File_close 방식으로 반복문을 돌려 일괄처리 하는 방법을 생각했다.


그러다가 문득 든 생각이,  

**'애초에 Jeykyll-import 로 파싱해서 처음 생성할때부터 잘만드면 되는거 아니야? 파일 파싱해서 생성하고, 그걸 또 열어서 수정해야되고 두번이나 작업을 거쳐야돼?'** 였다.



바로 jeky-import 라이브러리의 blogger.rb 파일을 수정하려 들었다.
(VScode를 이용해서 작업했다.)

blogger.rb 파일의 경로는 다음과 같다.

###### C:\Users\user\AppData\Local\Packages\CanonicalGroupLimited.UbuntuonWindows_79rhkp1fndgsc\LocalState\rootfs\home\우분투계정\gems\gems\jekyll-import-0.20.0\lib\jekyll-import\importers\blogger.rb


파일을 열어서 author를 검색했다.

header ~~ 밑에 각 value : key 값을 적는 코드들이 있는데 이부분을 수정해주면 될거 같다.

minimal_mistakes 테마는 author 밸류가 없으니 그냥 주석처리했다.

layout : post 항목도 그냥 주석처리했다. layout : single 로 써도 상관없다.


![layout_author](/assets/image/posts_image/post_movd_2/layout_author.png)


아마 자신의 포스트글 header 양식에 맞추어 입맞대로 일괄적으로 수정하려면 이 line을 입맞대로 바꾸면 될거같다.


파일을 저장하고

다시 cmd \-> bash \-> jeykyll-import 명령어 실행을 해서 백업본.xml 파일을 파싱해서 포스트글.html 파일들을 생성했다.

파일을 열어보니 정상적으로 author 와 layout 밸류가 지워져 있음을 확인했다.


![layout_author2](/assets/image/posts_image/post_movd_2/layout_author2.png)



여기서 문제가 하나 발생했다.

구글 블로그는 tags 만 있고 category 는 없는데 minmal_takes 테마는 category 가 있다는 것이다.

category 는 일괄적으로 처리할수 있는게 아닌, 포스트글 내용을 직접보고 그에 알맞은 category 를 부여 해야한다.



하지만 글들의 내용만 알면, 내 홈페이지 category 에 맞추어 폴더별로 만들어 category를 일괄적으로 넣어주는 작업은 할수 있을것 같다.


결국 각각의 포스트글들에 알맞은 category 를 부여하기 위해 파이썬 코드를 작성한다.
