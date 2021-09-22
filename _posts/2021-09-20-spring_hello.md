---
title: "[spring] 튜토리얼(4). 스프링 부트 없이 헬로월드 출력하기"
tags:
- spring
- java
categories:
- srping
date: '2021-09-20 06:00:57'
classes: wide
---

### 메이븐 혹은 그레이들 프로젝트 생성 후, spring 의존 설정 끝냈다고 가정함

<br>
<br>

## Step1. 필요 소스파일

다음과 같은 소스파일을 src/main/java 소스폴더에 생성한다. 패키지 이름은 자유.

- Greeter.java : 문자열 2개 입력받고 데이터 포맷으로 하나로 합치고, 문자열로 다시 리턴하는 클래스

- AppContext.java : 스프링 설정 파일, Greeter 클래스를 생성해 리턴하는 메소드를 bean 객체로 설정

- Main.java : 스프링 실행, bean 객체를 얻어와서 문자열 입력후 콘솔에 출력

<br>
<br>

**AppContext.java**

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

//@Configration : 해당 클래스를 스프링 설정 클래스로 지정할수 있음
@Configuration
public class AppContext {


	@Bean
	public Greeter greeter() {
		Greeter g = new Greeter();
		g.setFormat("%s, 안녕하세요!");
		return g;
	}

}
```

-