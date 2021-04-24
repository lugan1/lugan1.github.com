---
title: "[github pages] jekyll_admin 에서 자동으로 date, 수정된 날짜 넣는방법"
tags:
- github pages
- ruby
- jekyll_admin
categories:
- github pages
date: '2021-04-24 09:38:51 +0900'
last_modified_at: '2021-04-24 21:25:36 +0900'
---

먼저 코드를 수정을 할려면 텍스트 편집기나 에디터가 필요하다.
(나는 VScode 로 수정했다.)


Vscdoe 로 다음과 같은경로로 들어가서 폴더째로 연다.

C:\Ruby30-x64\lib\ruby\gems\3.0.0\gems\jekyll-admin-0.11.0


그 다음에 다음과 같은 파일들을 수정한다.

C:\Ruby30-x64\lib\ruby\gems\3.0.0\gems\jekyll-admin-0.11.0\lib\jekyll-admin\apiable.rb


![date](/assets/image/posts_image/jekyll_admin_date/apiableRB.png)


content_filed 함수 부분에서 다음과 같은 코드를 추가한다.

```ruby
front_matter\["last_modified_at"] = Time.now
```

front_matter 해시에서 modified_date 를 key로 하고, 현재시각을 value 로 하는 값을 추가한다는 뜻이다.

\_include\page_date.html 파일에서 last_modified_at 으로 되어있어서 last_modified_at 으로 한다. 다른 key로 하고싶으면 파일 둘다 key 이름을 통일시키면 된다




코드를 추가했으면 그 다음에 다음과 같은 파일을 수정한다.

C:\Ruby30-x64\lib\ruby\gems\3.0.0\gems\jekyll-admin-0.11.0\lib\jekyll-admin\server.rb


![date](/assets/image/posts_image/jekyll_admin_date/serverRB.png)


document_body 함수에서 다음과 같은 코드를 추가한다.

```ruby
if new? :
		body << "\ndate: #{Time.now}"
end
```

파일이 처음만드는거면 date: 현재시각 문자열을 body 에 추가하라는 뜻이다.


수정을 완료하고 저장을 한뒤에, 로컬서버를 다시 구동시키고 admin 페이지에서 포스트글을 작성, 수정하면 date와 modified_date가 현재시각으로 추가될것이다.

(Ruby 하나도 모르는데 맨땅부터 시작하느라 몇일 고생했다 ㅠ)
