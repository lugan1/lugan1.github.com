---
title: "[ionic] 아이오닉 설치 및 빌드하는 방법"
tags:
- ionic
categories:
- ionic
date: '2021-11-05 09:50:00'
classes: wide
---

# 아이오닉 설치 및 빌드 하는 방법
- 터미널에서 다음과 같이 명령어 입력

```
npm install -g ionic
```

<br/>

## \[PowerShell] PSSecurityException : UnauthorizedAccess
- 해결방법 :  
https://extbrain.tistory.com/118  

- 관리자 권한으로 PowerShell 실행
- 다음과 같은 명령어 입력
```
Set-ExecutionPolicy Unrestricted
```

<br/>
<br/>

- 다음과 같은 명령어로 ionic 생성후 빌드
```
ionic start
```

<br/>
<br/>

- 생성된 app 프로젝트로 이동 cd 명령어 사용
- 생성된 app 프로젝트로 이동 후 다음과 같은 명령어로 빌드

```
ionic serve
```


- tab : 밑에 탭 버튼이 있는 상태로 아이오닉 생성

<br/>
<br/>

# 기존의 프로젝트를 ionic 으로 변환하는 방법
- 다음과 같은 명령어로 native run 설치
```
npm i -g native-run
```

<br/>
<br/>

- 다음과 같은 명령어로 cordova 설치
```
npm i -g cordova
```

<br/>
<br/>


- 프로젝트 최상위 폴더에서 다음과 같은 명령어를 실행한다.
- 아이오닉 패키지를 지금 하고있는 프로젝트로 갖고온다.
```
ng add @ionic/angular
```

<br/>
<br/>

- 아이오닉으로 기존 프로젝트를 초기화한다.
- 프로젝트 이름을 물어보는데 현재 프로젝트 이름을 동일하게 입력해야 된다.
```
ionic init
```

- angular.json파일에서 outputPath "dist/\[프로젝트이름]"을 "www" 로 변경하여 www용 Ionic 프로젝트를 빌드할 폴더를 설정한다.

<br/>

-  index.html 파일에서 \<base href=”/”>를 \<base href=”./”> 로 변경한다. 
   - \<base href=””>는 모든 상대 URL의 기본 URL을 문서로 정의하고 기본적으로 루트로 설정된다.


<br/>
<br/>

- 다음과 같은 명령어로 ionic 으로 프로젝트를 build한다.
```
ionic serve --project="현재프로젝트이름"
```

<br/>
<br/>


# ionic cordova로 실행하는 방법
- 다음과 같은 명령어를 입력한다
```
ionic cordova run android --project="현재프로젝트이름"
```

<br/>

- 빌드된 Android APK는 플랫폼의 루트 폴더에서 찾을 수 있다.
- "platforms\android\app\build\outputs\apk\debug"로 이동할 수 있다.
- 휴대폰을 통해 설치하거나 에뮬레이터를 활성화하여 Ionic 모바일 앱을 볼 수 있다.



<br/>


## 다음과 같은 error 해결방법
```
Requirements check failed for JDK 1.8.x! Detected version: 17.0.0
Check your ANDROID_SDK_ROOT / JAVA_HOME / PATH environment variables.
[ERROR] An error occurred while running subprocess cordova.

        cordova.cmd build android exited with exit code 1.

        Re-running this command with the --verbose flag may provide more information.

```
- **JDK 1.8 버전 필요**
- JDK 설치후, 환경변수 세팅, 윈도우 재시작 필요

<br/>
<br/>
<br/>


- 다음과 같은 error 해결방법

```
FAILURE: Build failed with an exception.

* What went wrong:
Could not determine the dependencies of task ':app:compileDebugJavaWithJavac'.
> Installed Build Tools revision 31.0.0 is corrupted. Remove and install again using the SDK Manager.
```
- 안드로이드 스튜디오 -> tools -> SDK Mnager 로 31.0.0 버전 설치/제거

