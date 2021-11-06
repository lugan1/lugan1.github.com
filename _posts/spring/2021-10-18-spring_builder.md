---
title: "[spring] 스프링 Builder Pattern "
tags:
- log
- spring
categories:
- spring
date: '2021-10-18 03:26:00'
classes: wide
---

# 참고 및 출저 사이트 :  
[https://zorba91.tistory.com/298](https://zorba91.tistory.com/298)


<br/>
<br/>

# Spring LoomBook Builder Pattern
- 어떤 객체를 생성할때마다, 필드 값에 접근할면 각 필드값마다 getter, setter 를 설정해줘야 되는데, Builder 어노테이션을 사용하면 간편하게 필드값을 설정해 객체(VO)를 만들 수 있다.

- 객체들마다 들어가야할 인자가 각각 다를 때 유연하게 사용할 수 있다.

- 무조건 setter 생성을 방지하고 불변객체로 만들 수 있다.

- 필수 argument를 지정할 수 있다.(보통의 경우, PK 역할을 할 Id 값이 될 것이다.)

사용예제)

**객체 VO**
```java
//객체클래스 위에다가 @Builder 어노테이션을 붙인다.
@Data
@Builder
public class StudyBoardHeader {
    long id;
    String search_option;
    String search_word;
    int total;
    int offset;
    List<StudyBoard> items;
    //items 에는 Board VO들의 값이 들어있는 리스트가 들어간다

        /**
     * 클래스명Builder builder(매개변수) {
     *     return new 클래스명Bulder().필드(매개변수);
     * }
     * 형식으로 null이 들어가면 안되는 필수 key 값을 설정할수 있다.
     * 
     */
    public static StudyBoardHeaderBuilder builder(Long id) {
        if(id == null) {
            throw new IllegalArgumentException("필수 파라미터 누락");
        }
        return new StudyBoardHeaderBuilder().id(id);
    }
}
```

<br/>
<br/>


**객체 생성**
```java
        StudyBoardHeader.builder(145L)
                .search_option(search_option)
                .search_word(search_word)
                .offset(page_offset)
                .items(items)
                .total(count)
                .build();
```
- 필수 값 Key는 .builder(매개변수) 값으로 넣어서 생성할 수 있다.
- 필드.(필드 설정값) 으로 각 필드에 대한 값들을 설정하고, .build() 를 마지막에 사용하면 객체 VO가 자동으로 생성된다.