---
title: "루비 커맨드 명령어 정리"
tags:
- ruby
- github pages
- migration
- blogger
- jekyll
categories:
- github pages
- ruby
---

이전 포스트에서 구글 blogger -> 깃허브 페이지 로 포스트글 이전하려면 ruby 명령어를 알아야 될거같아서 공부한거 정리한다.

[[github pages] 구글 블로그 에서 깃허브 블로그로 이전하는 방법](https://lugan1.github.io/github%20pages/migration/)

---
```
사용법 : ruby [switches] [-] [programfile] [arguments]
  -0 [8 진수] 레코드 구분 기호 지정 (인수가없는 경우 \ 0)
  -a -n 또는 -p를 사용하는 자동 분할 모드 ($ _를 $ F로 분할)
  -c 구문 만 확인
  -Cdirectory 스크립트를 실행하기 전에 디렉토리로 cd
  -d 디버깅 플래그 설정 ($ DEBUG를 true로 설정)
  -e '명령'한 줄의 스크립트. 여러 개의 -e가 허용됩니다. [프로그램 파일] 생략
  -Eex [: in]은 기본 외부 및 내부 문자 인코딩을 지정합니다.
  -자동 분할 (-a)을위한 Fpattern split () 패턴
  -i [확장자] ARGV 파일을 제자리에서 편집 (확장자가 제공된 경우 백업)
  -Idirectory는 $ LOAD_PATH 디렉토리를 지정합니다 (두 번 이상 사용할 수 있음).
  -l 줄 끝 처리 활성화
  -n 'while gets (); ... 스크립트를 둘러싼 루프 종료
  -p -n과 같은 루프를 가정하지만 sed와 같은 라인도 인쇄합니다.
  -rlibrary는 스크립트를 실행하기 전에 라이브러리가 필요합니다.
  -s 스크립트 이름 뒤의 스위치에 대해 일부 스위치 구문 분석을 활성화합니다.
  -S PATH 환경 변수를 사용하여 스크립트를 찾습니다.
  -v 버전 번호를 인쇄 한 다음 상세 모드를 켭니다.
  -w 스크립트에 대한 경고를 켭니다.
  -W [level = 2 | : category] 경고 수준을 설정합니다. 0 = 무음, 1 = 중간, 2 = 상세
  -x [디렉토리] #! ruby ​​라인 앞의 텍스트를 제거하고 디렉토리로 cd
  --jit 기본 옵션으로 JIT 활성화 (실험적)
  --jit- [option] 옵션으로 JIT 활성화 (실험적)
  -h이 ​​메시지를 표시합니다. --help for more info
```


#### 루비 문법정리
-------------

yield 사용 간단예제

```ruby
def my_method
  puts "reached the top"
  yield
  puts "reached the bottom"
end
my_method do
  puts "reached yield"
end
```

<br> 루비는 함수 실행시에 함수이름 do 하고 실행하는듯
