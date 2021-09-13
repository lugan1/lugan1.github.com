---
title: "[javascript] 간단 예제"
tags:
- javascript
categories:
- javascript
date: '2021-09-13 12:17:57 +0900'
classes: wide
---

## 자바스크립트로 간단 실행문 작성

1. 비쥬얼 스튜디오 코드에서 Ctrl+N 으로 새문서 작성.

2. 파일 이름을 ~~.html 확장자로 저장

3. html:5 입력후 TAB을 누르면 body 영역을 제외한 부분이 자동으로 입력됨.

4. 다음과 같은 간단예제 코드 입력


```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scal=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>맛보기 예제</title>
</head>
<body>
    <script>
        //여기서부터 javascirpt 코드 시작

        var age = prompt("당신의 나이는?", "0");
        if(age >= 20){
            document.write("당신은 성인입니다.");
        } else {
            document.write("당신은 미성년자입니다.");
        }
    </script>
</body>
</html>
``` 

5. 완료된 파일을 직접 크롬브라우저로 열거나, Ctrl+ Alt+ O를 눌러 크롬브라우저로 열음