---
title: "[spring] My-batis 동적 SQL, CDATA"
tags:
- log
- spring
categories:
- spring
date: '2021-10-13 17:16:00'
classes: wide
---

# MyBatis의 동적 SQL
- if문, 구문을 지정해서 불러오기 재사용 등의 기능

<br/>
<br/>

# mybatis-SQL.xml 에 SQL 모듈로 해서 재사용, if문 사용방법
- SQL 전체가 아니라 SQL 에서 작은 구문만 지정해서 구문을 불러올 수도 있다.


<br/>
<br/>

## SQL 모듈로 만들어서 다른 SQL 에서 불러와서 재사용 방법
- SQL id 를 지정한다. SQL 태그로 감싼 sql 이 실행된다.
- include refid='SQL id' 태그로 지정된 ID의 SQL 를 불러온다.

```xml
<sql id="testSQL">
    and title like concat("%", "TestWord", "%")
</sql>


<select>
 select *
 from lee_board
 where state = 1
<include refid="testSQL"/>
```

- 이렇게 하면 testSQL 의 SQL구문이 include 와 바인딩되어 들어간다.

<br/>
<br/>

# MyBatis의 표현식
# 참조 및 참고 사이트 :  
[https://doublesprogramming.tistory.com/202](https://doublesprogramming.tistory.com/202)

- 태그 안에서 다음과 같은 속성들을 사용한다.
- test = "조건식"
- prefix="구문", prefixOverrides="구문"
- item, index, collection, open 등의 속성을 사용

## MyBatis의 표현식 종류
- if : 조건문 처리.
  - \<if test="조건문"> SQL구문 </if>

  <br/>

- choose : switch 와 같은 상태에 따른 조건문 처리
  - 예제)
  ```xml
    <choose>
        <when test="조건문">
            SQL 구문
        </when>
        <when test="조건문">
            SQL 구문
        </when>
        <otherwise>
            SQL 구문
        </otherwise>
    </choose>
  ```

- trim : 로직을 처리하면서 필요한 구문을 변경함
- foreach : 컬렉션에 대한 순환처리


<br/>
<br/>

# Mybatis CDATA
## 출저 및 참고 사이트 :  
[https://epthffh.tistory.com/entry/Mybatis-%EC%97%90%EC%84%9C-CDATA-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0](https://epthffh.tistory.com/entry/Mybatis-%EC%97%90%EC%84%9C-CDATA-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)

- SQL 구문에서 > 와 같은 기호가 닫는 괄호인지, 비교 연산자인지 xml 에서 구분이 안되서 사용
- 이 외에도 마이베티스의 맵퍼.xml 특수문자를 사용하는데 제약이 있다.

- CDATA 를 사용하면 CDATA 태그 안에서는 전부 문자열로 치환된다.
- \<\!\[CDATA\[ **SQL의 부분구문** ]]> 방식으로 사용한다.

<br/>
<br/>

예제)
**CDATA 사용 (X)**
```xml
<select id="findAll" resultMap="MemberResultMap">
    select *
    from employees 
    where salary > 100
</select>
```
- 해당 SQL 은 오류가 난다. 부등호 > 가 닫힘 태그로 인식이 되기 때문이다.

<br/>
<br/>

**CDATA 사용**
```xml
<select id="findAll" resultMap="MemberResultMap">
    <![CDATA[
    select *
 
    from employees
 
    where salary > 100
    ]]>
</select>
```
- 중간에 조건문 태그를 감싸면 태그가 인식을 못한다.


<br/>
<br/>

**조건문 태그에서 CDATA 사용**
```xml
<select id="findAll" resultMap="MemberResultMap">
    <![CDATA[
    select *
 
    from employees
 
    where  1=1
    ]]>
    <choose>
        <when test='user_type != null and user_type =="1"'>
            <![CDATA[
                salary > 100
            ]]>
        </when>
 
        <otherwise>
            <![CDATA[
                salary < 100
            ]]>
        </otherwise>
    </choose>
</select>
```
