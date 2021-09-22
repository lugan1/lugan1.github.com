---
title: "[java] 어노테이션 개요, 만드는 방법"
tags:
- java
categories:
- java
date: '2021-09-20 06:24:57'
classes: wide
last_modified_at: '2021-09-22 09:00:01 +0900'
---

참고 및 출저 :
<br>

[https://www.youtube.com/watch?v=81U0MyuZQKo](https://www.youtube.com/watch?v=81U0MyuZQKo)

[https://elfinlas.github.io/2017/12/14/java-custom-anotation-01/](https://elfinlas.github.io/2017/12/14/java-custom-anotation-01/)

<br>

## Javadoc.exe 주석
- 해당 메소드, 클래스의 주석 /** 내용 */ 쓰면, javadoc.exe 가 따로 주석을 추출해서 문서를 만들어낼수 있음.


## Java 어노테이션(Annotation) 개요
-  JEE5(Java Platform, Enterprise Edition 5) 부터 새롭게 추가된 기능

- @문자열 형식으로 사용

- Junit (단위 테스트 프로그램) 이라는 특정 프로그램에게 정보 제공을 위한 기능(설정 정보) -> 예전에는 설정정보를 XML로 만들었음

- 자바가 기본적으로 제공하기도 하고, 유저가 직접 만들어서 사용할 수도 있음.

- 어노테이션은 컴파일시에 처리될 수도 있고, 런타임 후에 리플렉션을 이용해서 처리될 수도 있음.

- 어노테이션은 **소스코드에 붙이는 하나의 속성값, 이름표, 라벨**이라고 이해하면 쉬움


<br>

## 메타 어노테이션
- 어노테이션을 만들때 사용하는 어노테이션
- @Target, @Retention, @Inherited ...

<br>

## 사용자정의 어노테이션 만들고 사용하는 방법
- 기본적으로 어노테이션은 인터페이스에서 앞에 @만 붙은 형식이여서 인터페이스를 만들고, 기능구현은 따로 해줘야 함.

<br>

1. 어노테이션을 정의한다.
2. 원하는 타겟에 적용한다. (타겟 = 소스코드)
3. **어노테이션이 붙은 타겟을 어떻게 사용할지 기능을 구현한다.** (이부분 복잡할 수 있음)
4. 어노테이션이 붙은 클래스 객체를 생성하고, 그 클래스객체.getAnnotation(사용자정의어노테이션.class) 으로 어노테이션 객체를 가져와서 구현 및 값 사용

5. 해당 기능이 실행 될때, 타겟에 붙은 어노테이션에 따라서 타겟이 작동 된다.

<br>

### 어노테이션 정의

<br>

``` java
@Target(ElementType.Field)
@Retention(RetentionPolicy.RUNTIME)
public @interface 어노테이션이름 {
    자료형 추상메소드_이름();
    ...
    ...

}
```

<br>

ex)

```java
public @interface Test1 {
    String name();
    Int age();
    Int count();
    String[] testString();
    TesTtype testType(); //enum { First, Final }
    DateTime testDate(); //자신이 아닌 다른 애너테이션(@DateTime) 을 포함 시킬수 있다. 
}
```

<br>

사용 예)

```java
@Test1(
    name="hong" ,
    age = 30 ,
    count = 10 ,
    testString = { "spring", "winter" } ,
    testType = TestType.first;
    testDate = @DateTime(yymmdd="160101", hhmmss="235959" )
)
public class newClass { ... }
```

- 어노테이션의 추상 메소드는 구현 안해도됨. 값만 넣어도 됨
- Test 애너테이션 객체 생성후, test.name 하면 hong 값을 얻는 형식

<br>
<br>

ex)
```java
@Test1
public class newClass {
    public static void main(String args[]){
        Class<newClass> class_obj = newClass.class;
        //어노테이션이 붙은 클래스 객체 생성

        Test1 anno = class_obj.getAnnotation(Test1.class);
        // 어노테이션이 붙은 클래스 객체로부터 어노테이션 객체 가져옴
        // 한 클래스의 여러개의 어노테이션이 붙을수 있으니 매개변수로 가져올 어노테이션 지정해줘야됨
        // .getAnnotations() 하면 클래스에 붙은 모든 어노테이션을 가져옴

        String name = anno.name(); // "hong"

    }
}



<br>
<br>
<br>

사용 예2)

annotation.java
```java
public @interface test2 {
    Int count() default 30; //이와 같이 디폴트 값도 지정가능.
}
```


Main.java
```java
@test2 //default 값 지정하면 값 입력 안해도됨. 그럼 디폴트값이 설정됨
//@test2(count=30) 과 동일
public class Newclass { ... }
```

<br>
<br>


- 어노테이션의 요소가 하나고, 이름이 value 일때는 요소의 이름 생략 가능

사용 예3)
```java
public @interface test3 {
    String value();
}


....

@test3("namename") // test3(value="namename") 과 동일
public class newClass{ ... }
```


<br>
<br>

### **@Target** : 말 그대로 어노테이션의 타겟을 지정함. 
<br> (타겟 = 소스코드 유형)

<br>

ElementType 클래스의 상수값들

|이름|적용대상|
|---|---|
|TYPE|클래스, 인터페이스 등|
|ANNOTATION_TYPE|어노테이션|
|FIELD|멤버 변수|
|CONSTRUCTOR|생성자|
|METHOD|메소드|
|LOCAL_VARIABLE|로컬 변수|
|PACKAGE|패키지|
|PARAMETER|매개변수|
|TYPE_PARAMETER|타입-매개변수 (JDK 1.8)|
|TYPE_USE|타입이 사용되는 모든 곳 (JDK 1.8)|


<br>
<br>

### **@Retention** : 어노테이션의 지속기간. 
 - 해당 어노테이션을 소스코드에서 단순 주석으로 사용할지, 컴파일 시기까지 유지할지, 런타임까지 유지할지 결정할수 있음

 - 보통 어노테이션은 RUNTIME 에 많이 사용되므로 대부분의 어노테이션은 RUNTIME 으로 설정되어있음

 <br>

RetentionPolicy 클래스의 상수 값들

<br>

|이름|설명|
|------|------|
|SOURCE|소스상에서만 정보 유지, 소스코드 분석시에만 의미가 있으며 바이트 코드 파일에는 정보가 남지 않음. 컴파일 전까지만 유효, 컴파일 이후에는 사라짐|
|CLASS|바이트 코드 파일까지 어노테이션 유지, 리플렉션을 사용하여 어노테이션 정보를 얻을수 없음. 컴파일러가 클래스를 참조할때까지 유효|
|RUNTIME|바이트 코드 파일까지 어노테이션 정보 유지, 리플렉션을 이용해서 어노테이션 정보를 얻을수 있음. 컴파일 이후에도 JVM에 의해 계속 참조 가능 (리플렉션 사용)|

 <br>
 <br>

예) @Override -> Retention값 Source 임. 컴파일러가 소스코드가 올바르게 오버라이딩 됬는지 컴파일전에 체크하는거니까 런타임에는 필요없음

 <br>
 <br>


### **@Documented** : 해당 어노테이션을 Javadoc에 포함시킴

### **@Inherited** : 어노테이션의 상속을 가능하게 함

### **@Repeateble** : Java 8 부터 지원하며, 연속적으로 어노테이션을 사용할 수 있게 해줌

<br>
<br>
<br>

## 마커 어노테이션
- 요소가 하나도 없는 어노테이션
- ex) @override, @Test, @Deprecated ....

<br>
<br>

## 리플렉션과 어노테이션을 사용한 예제

출저 : [https://elfinlas.github.io/2017/12/14/java-custom-anotation-01/](https://elfinlas.github.io/2017/12/14/java-custom-anotation-01/)

<br>
<br>

**Testannotation.java**

```java

import static java.lang.annotation.ElementType.FIELD;
import static java.lang.annotation.RetentionPolicy.RUNTIME;

import java.lang.annotation.Retention;
import java.lang.annotation.Target;

@Retention(RUNTIME)
@Target(FIELD)
public @interface TestAnnotation {
	int data() default 0;
}
```


<br>
<br>

**Implements_Annotation.java**

```java

import java.lang.reflect.Field;
import java.util.Optional;

public class Implements_Annotation {
	
    private <T> T checkAnnotation(T targetObj, Class annotationObj) {
        Field[] fields = targetObj.getClass().getDeclaredFields();
        //매개변수로 타겟 객체가 오면, 그 객체의 선언된 변수들을 갖고옴.(리플렉션), 그리고 Field 자료형인 fields 컬렉션에 넣음
        
        for (Field f : fields) {
        	//fields 객체의 요소들 갯수 동안 반복문 돌림
            if(annotationObj == TestAnnotation.class) {
            	//만약 매개변수(오브젝트) annotationObj 가 TestAnnotation 클래스면
                return checkAnnotation4InsertInt(targetObj, f);
                //checkAnnotation4InsertInt 메서드실행
            }
        }
        return targetObj;
    }
    
    // for (A : B) -> B 에서 차레대로 꺼내서 A 에다가 넣음. B에서 꺼낼 객체가 없을때까지

    
    //checkAnnotation 에서 return 할때 실행.
    private <T> T checkAnnotation4InsertInt(T targetObj, Field field) {
    	TestAnnotation annotation = field.getAnnotation(TestAnnotation.class);
    	// 인자로 받은 field객체에서 어노테이션을 가져와서 -> 어노테이션 객체 생성해서 넣음
    	
        if(annotation != null && field.getType() == int.class) {
        	// annotation 이 null 이 아니고, 받은 매개변수 변수객체의 타입이 Int 자료 형이면
        	
            field.setAccessible(true);
            // private의 변수, 메소드 등 요소에 접근할려고 할때 보통은 접근 못하지만 리플렉트의 setAccessible() 메소드로 접근 가능하게 해줌.
            
            try {
            	field.set(targetObj, annotation.data()); 
            	// 해당 변수의 값을 어노테이션 값으로 바꿈
            	// 받은 매개변수의 값을 바꿈.
            	// testAnnotation 인터페이스의 data() 변수. 즉 0 으로.
            	
            }
            catch (IllegalAccessException e) { System.out.println(e.getMessage()); }
        }
        return targetObj;
    }
    
    
    public <T> Optional<T> getInstance(Class targetClass, Class annotationClass) {
    	//매개변수 1 : 어노테이션 적용 클래스, 매개변수 2 : 어노테이션 인터페이스 클래스
        //두개의 클래스를 매개변수로 checkAnnotation() 메소드 실행, -> 
    	//checkAnnotation() 메소드는 checkAnnotation4InsertInt 메소드 실행 (필드 변수값 어노테이션 설정값으로 바꿈)
    	//마지막으로 Optional 로 바꿔서 리턴
    	
    	Optional optional = Optional.empty();
        Object object;
        try {
            object = targetClass.newInstance();
            object = checkAnnotation(object, annotationClass);
            optional = Optional.of(object);
        }catch (InstantiationException | IllegalAccessException e) { System.out.println(e.getMessage()); }
        return optional;
    }
    
}
```

<br>
<br>

**UseAnnotation.java**

```java
public class UseAnnotation {
	
	@TestAnnotation(data= 30)
	private int Data_one;
	
	@TestAnnotation
	private int Default_data;
	
	public UseAnnotation() {
		
		this.Data_one = -1;
		this.Default_data = -1;
	}

	public int getData_one() {
		return Data_one;
	}

	public int getDefault_data() {
		return Default_data;
	}


	
}
```

<br>
<br>

**main.java**
```java
package hello_gradle;

import java.util.Optional;

public class main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub

        Implements_Annotation handler = new Implements_Annotation();
        UseAnnotation exam01 = handler.getInstance(UseAnnotation.class, TestAnnotation.class)
                .map(item -> (UseAnnotation)item)
                .orElse(new UseAnnotation());
        
        
        // map-> 자바 optional 에서 새롭게 추가 된 Optional 객체 메소드
        // orElse -> 자바 optional 에서 새롭게 추가된 Optional 메소드
        // optional -> java8 에서 새롭게 도입된 신기능. null 대신 optional 값으로 표현함. 
        // 즉 이전버전까지의 nullPointException 을 해결하기 위해 등장한 방법
        
        // map -> Optional 안에 래핑된 계산 결과를 반환함. 그런다음 반환된 Optional 객체에서 적절한 메서드를 호출하여 값을 검색해야됨
        // orElse -> Optional 객체에 맵핑된 값이 존재하면 그 값을 리턴하고, 그렇지 않으면(null 이면) 기본값으로 전달된 매개변수 값을 리턴함
        // 즉, Java8 에서 생긴 Optional은 값이 없는 상황을 처리할 방법을 만듬. 1. 기본값반환 2. 예외 던지기
        
        
        // map(item -> (UseAnnotationitemo -> 각각에 있는 아이템들을 꺼내서 item 이라는 변수로 치고, (UseAnnotation) 으로 형변환함
        // 파이썬의 for item in list 이거랑 비슷함
        // .map(person::getAddress) -> .map(person.getAddress) 이거랑 같음. 람다식 주일려고 :: 쓰는거임
        

        System.out.println("myAge = " + exam01.getData_one());
        System.out.println("defaultAge = " + exam01.getDefault_data());

		
	}

}
```



