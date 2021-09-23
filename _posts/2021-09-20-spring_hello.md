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

<br/>
<br/>

**AppContext.java**

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

//@Configration : 해당 클래스를 스프링 설정 클래스로 지정할수 있음
@Configuration
public class AppContext {

	//@Bean : 이 어노테이션이 달리면 해당 메서드가 생성한 객체를 스프링이 관리하는 빈 객체로 등록함
	@Bean
	public Greeter greeter() {
		Greeter greeter = new Greeter();
		greeter.setFormat("%s, 안녕하세요!");
		return greeter;
	}

}
```

<br/>
<br/>

**Greeter.java**

```java
public class Greeter {
	private String format;
	
	public String greet(String guest) {
		// 매개변수 guest 가 들어오면 format %s 같은 포맷 문자와 함께 문자열로 치환되서 출력
		return String.format(format, guest);
	}
	
	public void setFormat(String format) {
		// %s 같은 포맷이 포함된 문자열이 들어오면 현재 클래스의 format 문자열에 대입
		this.format = format;
	}
	
}
```


<br/>
<br/>

**Main.java**

```java
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

public class Main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		AnnotationConfigApplicationContext applicationcontext = new AnnotationConfigApplicationContext(AppContext.class);
		//독립 실행형 어플리케이션 콘텍스트 객체.
		//매개변수는 @Configuration 어노테이션이 설정된 스프링 설정클래스
		//스프링 설정 클래스에서 정의한 @Bean 설정 정보를 읽어와 객체를 생성하고 초기화한다. 
		
		Greeter greeter = applicationcontext.getBean("greeter", Greeter.class);
		//getBean : @Bean 객체를 가져올때 사용
		//파라미터1 : @Bean 애노테이션 메서드 이름인 Bean 객체의 이름
		//파라미터2 : 가져올 Bean 객체의 타입 (클래스)
		
	}

}
```