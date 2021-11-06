---
title: "[angular] 모듈 추가시에 class is not an angular module 해결방법"
classes : wide
tags:
- angular
- error
categories:
- angular
date: '2021-10-12 10:39:00'
---

# 참조 및 참고 사이트 :  
[https://stackoverflow.com/questions/58437137/class-is-not-an-angular-module-only-in-intellij-webstorm-when-importing-locall](https://stackoverflow.com/questions/58437137/class-is-not-an-angular-module-only-in-intellij-webstorm-when-importing-locall)

<br/>

### Ngx-Editor 모듈을 공식홈페이지 나온대로 터미널에서 npm 인스톨을 해서 앵귤러에 추가했는데, app-modules.ts 에 추가시에 계속 빨간줄이 뜨면서 class is not an angular module 이라고 뜨는것이다. 해결방법 찾느라 2시간정도 걸렸다.

<br/>
<br/>


# Angular 모듈 추가시에 class is not an angular module 뜨는 문제 해결방법
- intellij 에서 Ctrl+Shift+A 눌른다
- Registry 를 검색한다. 더블클릭한다.
- 여러개 뜨는 옵션 항목중에서 angular.enableIvyMetadataSupport 를 체크한다.
- IntelliJ IDE를 재시작한다.
- App-modules.ts 파일에 빨간줄 사라지는것 확인. 컴파일 실행시에 정상적으로 임포트되어 웹에 모듈 표시되는것 확인