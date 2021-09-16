---
title: "[spring] 스프링 환경세팅, 설치할것"
tags:
- spring, java
categories:
- srping
date: '2021-09-17 01:31:57'
classes: wide
---

## 스프링 환경세팅, 설치 준비물

1. JDK 설치 및, JAVA_HOME 환경변수 설정
<br> [오라클 홈페이지](http://www.orcale.com)
<br>  환경변수 설정
   - step 1. C:\Program Files\Java\jdk 설치된곳/bin 으로 가서 경로 복사
   - step 2. 시스템 고급설정-> 환경변수에서 제일 위칸 새로 만들기에서 이름 : JAVA_HOME, 변수값 : 아까 경로 복붙

   - step 3. 밑에 칸 path -> 편집 -> 새로만들기 -> %JAVA_HOME% 입력후 저장

   - step 4. cmd 에서 javac 치고 정상적으로 뜨는지 확인
<br>
<br>

2. 메이븐 설치 및, 환경변수 설정
<br> [아파치 메이븐](http://maven.apache.org)
   - step 1. 메이븐 압축파일 다운받기
   - step 2. c:/devtool/ 등 적당한곳에 압축파일 압축풀기 (설치 끝)

   - step 3. 시스템 고급설정 -> 환경변수 -> path 편집 -> 새로만들기 -> 압축푼 메이븐 bin 폴더 경로 복붙

   - step 4. cmd 에서 mvn -version 치고 정상적으로 뜨는지 확인
      - 에러 The JaThe JAVA_HOME environment variable is not defined correctly 뜰시에 해결법
      - (1)번 방법
      - 고급시스템 설정 -> 환경변수 설정에서, JAVA_HOME 경로를 bin 까지 해서 에러걸림. 즉 JDK 설치폴더 까지만 경로 복붙 편집
      - path 편집에서 %JAVA_HOME%bin 으로 수정 
      - (2)번 방법
      - CMD 창에 set JAVA_HOME= (jdk가 설치된 경로) 입력

<br>
<br>

3. 그레이들 설치 및, 환경변수 설정
<br> [그레이들](https://gradle.org/releases)
   - step 1. 그레이들 압축파일 다운받기
   - step 2. c:/devtool/ 등 적당한곳에 압축파일 풀기 (설치 끝)
   - setp 3. 고급 시스템설정 -> 환경변수 -> path 편집 -> 새로만들기 -> 압축 푼 그레이들 bin 폴더경로 복붙

<br>
<br>


4. 이클립스 설치
<br> [이클립스](http://www.eclipse.org/)
    - 새 프로젝트 -> JAVA 프로젝트 -> new class -> main() 추가설정 -> 확인 -> system.out.println("hello world"); 정상출력 확인