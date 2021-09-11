---
title: "[java 복습(1)] 접근제한자, instanceof, java doc, 상속 "
tags:
- java
categories:
- java
date: '2021-09-10 10:04:57 +0900'
classes: wide
last_modified_at: '2021-09-11 20:44:01 +0900'
---
21년 09월 10일, JAVA 책을 오랜만에 다시 피고, 중요 개념들을 포스트하면서 정리하는 시간을 가졌다.

<br>
<br>

## 접근제한자
**public** - <u>어느 클래스 에서나</u> 접근 가능

**protected** - <u>같은 패키지 내 클래스 및 상속한 클래스까지</u> 접근

**(제한자 없음)** - <u>같은 패키지 내 클래스까지</u> 접근 (default or friendly)

**prvate** - <u>자신의 클래스 내에서만</u> 접근가능

<br>

## java doc
- 주석을 바탕으로 클래스와 메서드 등에 관한 설명을 HTML 형식으로 출력해주는 기능
- ex) /** @parm args */
- @parm : 태그, 주석에 의미 부여 가능

<br>

## static
static 변수
- 클래스에서 인스턴스를 몇개 만들어도 메모리에는 단 하나만 생성됨 (중요)
- 모든 인스턴스에서 같은 값을 공유함.

<br>

static 메서드
- 인스턴스의 상태와 관계 없이 지정된 처리를 하기위한 메서드

```java
static 자료형 메서드명 (자료형 인수명){
    내용
}
```

- static 변수와 메서드는 **인스턴스를 생성하지 않고 접근 가능**
- static 변수와 메서드에서 **static이 아닌 변수와 메서드에는 접근 못함**

<br>

## 메모리 영역
<br>

![mem](/assets/image/posts_image/2021_09_10_memory.jpg)

<br>

## 래퍼 클래스
- 기본 자료형(int, string ...) 등을 나타내는 클래스

<br>

## 자료형 비교 연산자 instanceof()
다음과 같을 경우에 true 반환
- 대상 데이터가 지정한 자료형의 인스턴스
- 지정한 클래스
- 지정한 클래스를 상속한 클래스
- 지정한 인터페이스를 구현한 클래스
- 사용 예시
<br>ex) (비교할 변수) **instanceof** (클래스...) ;
<br>ex) number **instanceof** testclass;

<br>

## 오버라이딩(overriding) 오버로딩(overloading) 차이
**오버라이딩(overriding)** - 자식 클래스에서 부모 클래스의 메소드 정의를 덮어씌어 다르게 동작하도록 재정의

**오버로딩(overloading)** - 같은 이름의 메소드를 매개변수에 따라 다르게 출력되도록 같은 이름의 메소드를 여러개 작성
```java
void cat() {
    내용
}

void cat(int a, int b){
    내용
}
```

## 상속(inheritance) 관련

- super 객체 -> 부모클래스
- 부모 클래스의 필드명이나 메서드명에 super라는 키워드를 붙여서 이용
<br> ex) super.work()


- 클래스, 메소드 선언시 **final 붙이면 자식클래스가 상속할 수 없게 됨**
- 부모클래스를 상속하면 **자식클래스의 생성자 객체만 호출해도 부모클래스의 생성자도 같이 실행됨**
<br>(자식클래스 생성자 맨 첫단에 super() 가 생략되어있기 때문)

- 부모클래스의 메소드 혹은 생성자에 인수가 있으면 **자식 클래스에서도 호출시 똑같은 인수를 넣어야 함**

