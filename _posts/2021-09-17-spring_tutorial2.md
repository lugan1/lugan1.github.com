---
title: "[spring] 튜토리얼(2). 그래들 프로젝트 생성"
tags:
- spring
- java
categories:
- srping
date: '2021-09-17 19:31:57'
classes: wide
last_modified_at: '2021-09-24 03:40:01 +0900'
---

저번 포스트에 메이븐 프로젝트를 생성하는 방법을 적었고, 이번에는 그래들 프로젝트를 생성하는 방법을 포스트 했다.

각각의 장단점이 있으며 

[메이븐(maven) vs 그래들(gradle) 프로젝트 차이](https://lugan1.github.io/java/maven_gradle/)

으로 따로 두개의 빌드 방법을 비교 공부했다. 결론은 그래들(Gradle)이 더 간결하고 짧은 문장으로 가독성이 있다고 한다.

<br>
<br>

## 그레이들 프로젝트 생성
- 메이븐 프로젝트와 별반 다르지 않다고 한다. 메이븐은 pom.xml 을 작성하고 그레이들은 build.gradle 파일을 작성한다.

<br>

### step 1. 
[help] -> [eclipse maketplace] -> gradle 검색 -> Buildship gradle integration 3.0 설치 되었는지 확인. 설치 안되었으면 설치

<br>

### step 2.
[Window] -> [Prefrences] -> [Gradle] -> local installation location 에서 그래들 압축 푼 폴더 설정


### step 3.
[file] -> [new] -> [other] -> [gradle prject] -> next -> 프로젝트 이름 입력후 next -> next -> finish

<br>

**could not execute build using connection to gradle installation** 오류 나올시에 해결방법
 - Gradle 공식 홈페이지에서 최신 버전을 다운받고 환경 변수 설정을 해준다.
 - 이클립스 Gradle 설정에서 로컬 디렉터리 경로를 아까 다운받은 최신 Gradle 경로로 잡아준다.

<br/>
<br/>

**Lib 하위폴더 생기는 문제 해결법**  
참고 :  
[https://stackoverflow.com/questions/65711292/gradle-build-two-projects-project-with-name-and-a-project-lib](https://stackoverflow.com/questions/65711292/gradle-build-two-projects-project-with-name-and-a-project-lib)  
[https://stackoverflow.com/questions/66005668/eclipse-gradle-wizard-creates-project-with-subfolder-lib](https://stackoverflow.com/questions/66005668/eclipse-gradle-wizard-creates-project-with-subfolder-lib)  
  
setting.gradle 파일에서 include('lib') 항목 삭제후 lib 폴더의 내용물을 전부 본래 프로젝트 폴더로 이동 -> lib 폴더 삭제

**현재 위 방법으로 문제 해결시에 project and external dependencies 사라지는 문제 발생** -> 그냥 lib 폴더에서 build-path 에서 junit , jre 라이브러리만 추가해서 해야됨


<br/>
<br/>


 자바 소스파일에서 **Implicit super constructor Object() is undefined for default constructor. Must define an explicit constructor** 오류 나올시 해결법
 - 왼쪽 익스플로러 창에서 프로젝트 마우스 오른쪽 버튼 클릭
 - build path -> configure buildpath -> Java build path -> Libraries 항목에서 add Library -> Jre system Library 선택후 저장

<br/>
<br/>



Gradle 프로젝트 파일 생성시, Lib 폴더와 프로젝트 폴더가 따로 보이는 현상 -> gradle 7.2 버전 문제인듯
 - gradle 7.2 이하로 내리면 프로젝트 자체가 생성이 안되서 현재로는 해결 불가


<br/>

Gradle 프로젝트 생성시 Lib 폴더에 빨간줄 쳐져있는 현상 해결법
 - Lib 폴더에 마우스 오른쪽 클릭 -> build path -> add Libraries -> JRE 추가하고 저장

<br/>
<br/>

**Gradle 프로젝트 이클립스 run 실행시 main 클래스 못찾는 오류 발생시 해결방법**
- 프로젝트 build_path 설정에서 Modulepath 항목에 JRE 추가, Classpath 항목에 Junit 추가하니 정상적으로 실행됬음


<br/>

### step 4. (만약 기존 프로젝트에 gradle import 할생각이면 여기서부터 시작. build.gradle 파일 부터 만듬)
스프링 의존(Dependencies) 설정하기
 - ~~build.gradle 파일 열어서 dependencies 의존에 'org.springframework:spring-context:5.0.2.RELEASE' 추가하기~~

 - 위 방법으로 하면 컴파일 시에 스프링 클래스 로드를 못한다고 예외 오류 뜬다. 다음과 같은 방법으로 해야된다.

   - [https://mvnrepository.com/artifact/org.springframework/spring-context](https://mvnrepository.com/artifact/org.springframework/spring-context) 공식 홈피에 들어간다.

   - spring-context 최신 버전 항목에 들어간다.

   - gradle-short 항목에 들어가서 implementation ~~ 하는 문장을 build.gradle에 복사 붙여넣기 한다.

   - 이클립스에서 gradle 리플래쉬 하면 최신 버전이 다운받아진다. 


 - 책에서는 앞에 compile 명령어가 붙지만 gradle 7버전 이상에서는 compile 명령어 사용하면 **Could not find method compile() for arguments** 오류 발생

 - compile 명령어 대신 implementation 명령어를 사용해야함  
 예시)

 ```
 implementation 'org.springframework:spring-context:5.0.2.RELEASE'
 ```
 
  - 입력 저장후, 프로젝트 마우스 오른쪽 클릭, gradle-> refresh gradle project

  - Project and external Dependencies 에 spring 관련 jar 파일들 다운로드 되어져 있는지 확인

<br/>
<br/>

### step 5. 
 CMD 창으로 프로젝트 폴더 이동해서 gradle wrapper 입력 실행
- 명령어 실행에 성공하면 프로젝트 루트 폴더에 다음과 같은 파일과 폴더가 생성된다.

- gradlew.bat 파일, gradlew 파일
   - 각각 윈도우와 리눅스에서 사용할 수 있는 실행파일
   - gradle 명령어 대신 사용할 수 있는 래퍼 파일
   - 이 래퍼파일을 사용하면 그래이들 설치 없이 그래이들 명령어를 실행 할 수 있음


- gradle 폴더

- 각 생성된 두개의 파일과 gradle 폴더를 공유하면 그래이들을 설치하지 않은 개발자도 생성한 래퍼 파일을 이용해서 그래이들 명령어를 실행할수 있음


<br/>
<br/>


### step 6.
 CMD 창으로 프로젝트 폴더 위치에서 gradlew compileJava 명령어 실행

### step 7.
 기존 프로젝트 폴더에서 [file] -> [import] 로 그래들 프로젝트 임포트





 
