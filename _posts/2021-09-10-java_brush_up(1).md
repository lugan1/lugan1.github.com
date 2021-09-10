---
title: "[java] 자바 중요개념 복습 (1) "
tags:
- java
categories:
- java
date: '2021-09-10 10:04:57 +0900'
classes: wide
---
21년 09월 10일, JAVA 책을 오랜만에 다시 피고, 중요 개념들을 포스트하면서 정리하는 시간을 가질려고 한다.

<br>
<br>

## 접근제한자
**public** - <u>어느 클래스 에서나</u> 접근 가능

**protected** - <u>같은 패키지 내 클래스 및 상속한 클래스까지</u> 접근

**(제한자 없음)** - <u>같은 패키지 내 클래스까지</u> 접근 (default or friendly)

**prvate** - <u>자신의 클래스 내에서만</u> 접근할 수 있음

<br>

## java doc
- 주석을 바탕으로 클래스와 메서드 등에 관한 설명을 HTML 형식으로 출력해주는 기능
- ex) /** @parm args */
- @parm : 태그, 주석에 의미 부여 가능

<br>

## static
static 변수
- 클래스에서 인스턴스를 몇개 만들어도 메모리에는 단 하나만 생성됨
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
- ex) (비교할 변수) **instanceof** (클래스...) ;
- ex) number **instanceof** testclass;

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
상속금지
- 클래스, 메소드 선언시 **final 붙이면 상속할 수 없게 됨**
