---
title: "[spring] 튜토리얼(1). 메이븐 프로젝트 생성, 프로젝트 파일구조"
tags:
- spring
- java
categories:
- srping
date: '2021-09-17 01:31:57'
classes: wide
---

## 메이븐 프로젝트 생성방법

[File] -> [new] -> [other] -> [maven project] ->

### \*archetype selection 뜻
- 메이븐 프로젝트 tool kit
- 메이븐 프로젝트에서 사용하는 모델이나 패턴을 템플릿화 해서 제공

<br>

기본 프로젝트로 생성할꺼니 skip 옵션 체크 -> 

<br>

## artifact 입력칸
- group ID -> 전체 프로젝트 제목 , arifact ID -> 작은 프로젝트 제목 이라고 봐도 될듯
- ex ) group ID : 태양계 시스템 프로젝트 , artifact ID : 지구 프로젝트

<br>

### gruop id
- 모든 프로젝트 중에서 나의 프로젝트를 식별하게 해주는 식별자
- groupid는 java 패키지 이름 규칙을 따라야 함. 즉, 제어하는 도메인의 이름을 반대로 시작
   - ex) org.apache.maven, org.apache.commons 
- 만약에 프로젝트가 다중 모듈 프로젝트인 경우 부모의 groupId에 새 식별자를 추가해 사용
   - ex) org.apache.maven, org.apache.maven.plugins, org.apache.maven.reporting


### artifact id
- 버전 없는 jar 파일의 이름
- 특수 문자 사용금지, 소문자로만 작성 가능
- 서드파티 jar 파일인 경우라면, 해당되는 이름만 사용해야 됨

### version
- 배포를 하려면 숫자와 점으로 구성된 일반적인 버전(1.0,1.1,1.0.1,...)인 형태를 사용해야 함
- SNAPSHOT (nightly) 빌드와 관련된 날짜 버전은 사용하지 않음 
- 서드파티 artifact 라면, 그들이 준 버전넘버를 사용해야 됨

------------------------------------

<br>

grup-id -> maven
<br> artifact-id -> hello_mvaen 입력후 finish

<br>
<br>

## 각 파일구조 설명

**src/main/java** :
- 자바 소스 파일, 기능 구현 하는 부분

<br>

**src/main/resources** :
- 보조파일들 , 스프링 설정파일 (xml), 프로퍼티 파일들이 모여있는 디렉터리

<br>

(웹어플리케이션 개발시) **src/main/webapp** :
- JSP 소스코드 , WEB-INF , web.xml 파일등이 들어있는 디렉터리

<br>

**Maven Dependencies** :
- 메이븐 의존에 설정한 (다운로드 한) 아티팩트가 이클립스 프로젝트의 클래스패스에 추가된것

- 여기에 있는 모든 jar 파일들은 메이븐 로컬 리포지토리 폴더에 위치함

<br>

**pom.xml** :
<br>
- 스프링 필요 모듈들을 명시하는 파일
- 각 모듈들을 명시하면, 원격지의 main repository 에서 자동 다운로드 

<br>

## pom.xml 파일 작성 
- 메이븐 의존 설정 추가
- 스프링의 각 모듈들을 가져오기 위한 파일이 pom.xml

- 메이븐은 코드를 컴파일하거나 실행 할때 \<dependency>로 설정한 아티팩트 파일을 사용한다.

- 메이븐이 \<dependency> 아티팩트 파일을 구하는 방법 두가지

   - (1). 메이븐 로컬 리포지토리에서 (그룹) \ (아티팩트) \ (버전) 폴더 경로에서 아티팩트ID-버전.jar 형식의 파일이 있는지 검사하고 파일 존재하면 사용
  
   
   - (2). 없으면 메이븐 원격 중앙 리포지토리에서 해당 파일을 다운로드, 로컬 리포지토리에 복사한뒤에 파일사용


<br>
<br>

## 메이븐 로컬 리포지토리 경로
- [사용자 홈 폴더] \ .m2 \ repository
- ex) C:\Users\사용자\.m2\repository


<br>

step 1. pom.xml 파일 열어서, \<version> 속성 밑에 다음과 같은 항목 추가
<br> \<denpendencies> \</dependencies> , \<build> \</build>

<br>

```xml
  	<dependencies>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-context</artifactId>
			<version>5.0.2.RELEASE</version>
		</dependency>
	</dependencies>
```
<br>

- dependcies : 뜻 그대로 이 모듈에 의존한다는 뜻
- groupID : org.springframework 에 있는
- artifacID : spring-context 모듈을 사용
- version : 사용하려는 모듈의 버전

<br>
<br>

## dependency(의존성)에 추가한 아티팩트 파일 경로
- 메이븐 로컬 리포지토리 \ (gruopID) \ (artifactID) \ (version)

- ex) [사용자 홈 폴더] \ .m2 \ repository \ org \ springframework \ spring-context \ 5.02.RELEASE

- 메이븐은 필요시에만 그때그때 원격 리포지토리에서 파일을 다운로드 하기때문에 열어보면 파일은 없음


<br>
<br>

## 실제로 원격 리포지토리에서 파일이 다운로드 되는지 확인하는 방법
- CMD 창으로 프로젝트 폴더 이동
- mvn compile 입력후 엔터
- 아티팩트 파일 경로에 가서 jar 파일이 생성 되었는지 확인
- 로컬 리포지토리에 아티팩트 파일을 다운로드 하면 이후에는 원격 리포지토리에서는 다운로드 되지 않음

<br>
<br>

## 메이븐 원격 리포지토리
- 메이븐을 관리하는 아파치 재단이 메이븐 중앙 리포지토리에 아티팩트 파일을 등록하는 방법등을 제공함

- 스프링을 비롯한 자바 개발에서 사용되는 많은 오픈 소스 프로젝트는 메이븐 중앙 리포지토리에 아티팩트 파일이 등록되어있음

<br>
<br>

## 의존 전이 (Transitive Dependencies)
- Dependency 에서 jar 파일 다운로드 하기에 앞서 pom 파일을 다운로드함

- pom 파일안에 dependency 속성이 여러개 있어서 필요파일들을 연쇄적으로 다운로드 하는것

- 의존한 아티팩트가 또다시 의존하고 있는 다른 아티팩드가 있다면 그 아티팩드도 함께 다운로드함

<br>
<br>

## spring-context 의존관계

### spring-context
 - spring-core
    - spring-jcl

 - spring-beans
 - spring-aop
   - aspectjweaver (optional)

 - aspectjweaver (optional)

<br>
<br>


## 메이븐 임포트가 안되어 있을시 메이븐 임포트 하는방법

 - Maven Dependencies 에 파일이 하나도 없으면 임포트가 안되어 있는것이다.

 - 왼쪽 패키지 탐색기에서 프로젝트 폴더 선택후 [File] -> [import] -> [Exiting Maven Projects]

 - 혹은 프로젝트 폴더 오른쪽 클릭후 Import -> Exiting Maven Projects

 - /porm.xml 체크후 finsih

 - Maven Dependencies 에 jar 파일들이 생겼는지 확인 