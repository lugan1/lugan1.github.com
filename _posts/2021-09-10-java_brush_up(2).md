---
title: "[java 복습(2)] 추상클래스, 인터 페이스, 제네릭, 람다, 익명 클래스"
tags:
- java
categories:
- java
date: '2021-09-12 00:58:57 +0900'
classes: wide
last_modified_at: '2021-09-12 19:47:01 +0900'
---

## 추상 클래스
- 추상 클래스 : 추상메소드를 포함하는 클래스
<br>(다른 메소드들의 처리구현 가능)

- 추상 메서드 : 이름, 반환형, 인수만 정희한 메서드.
<br>(처리할 내용은 자식 클래스에서 기술해야 함)

ex)
```java
//추상 클래스
public abstract class AbstractClassSample{
    abstract String sampleMethod(int i);
    //추상 메서드
    
    public void show(){
        system.out.println("hello world");
    }
}
```
<br>

- 추상 클래스를 상속한 경우 그 클래스에 있는 <u>추상 메소드는 반드시 구현해줘야 함</u>
- 여러명의 개발자끼리 파일구조 약속을 할 때 유용함

<br>
<br>
<br>

## 인터페이스
- 다중 상속 가능
<br>ex) implements InterfaceA, InterfaceB (둘다 구현해줘야 함)

- <u>추상 메서드만 있는 클래스</u>
- 모든 메소드가 추상이여서 상속하는 클래스는 다 구현(implements)해줘야 함

ex)
<br> Interface.class

```java
public interface InterfaceSample{
    abstract String sampleMethod1();
    abstract String sampleMethod2(int num);
}
```
<br>

ImplementsSample.class
```java
public class ImplementsSample implements InterfaceSample{
    public String SampleMethod1(){
        return "샘플 1";
    }
    public String SampleMethod2(){
        return "샘플2";
    }
}
```
<br>
<br>
<br>

## 위임
- 메소드 처리의 구현을 다른 클래스에 맡김
- 2개 이상의 클래스를 상속(다중 상속) 할 필요가 있는 자식클래스를 만들 경우 사용

Employee.class
```java
public class Employee{
    publoc void echo(){
        System,out.println("test");
    }
}
```
<br>

Manager.class
```java
public class Manager{
    Employee employee = new Employee();
    //extends를 안하고, 클래스 객체를 생성후, 그 클래스의 메서드를 실행.

    public void echo(){
        employee.echo();
    }
}
```

상속과 위임의 단점
1. 상속 계층이 깊으면 처리를 추적하기 어려움
 - 상속하고 싶지 않은 클래스에서는 final을 써서 상속을 금지하는 등 구현에 대해 연구해야 함

2. 부모클래스를 수정하면 자식 클래스에 영향을 미침
<br>
<br>
<br>
## 제네릭
- 클래스 내부에서 사용할 자료형을 미리 정의해 타입 세이프를 구현하는 기능
- 타입 세이프 : 다른 형의 값이 저장 되는 것을 막는 기능
- 자료형이 어떤것을 쓸지 정해지지 않을때도 사용
- 데이터 자료형을 매개변수로 사용가능

```java
// 제네릭 도입전
Lst list = new ArrayList();
list.add(13);
//아무 자료형이나 저장가능. 자료형이 object로 저장됨

int num = (Integer)list.get(0);
//object 자료형이라 형변환 필요



// 제네릭 도입후
List<Integer> list = new ArrayList(Integer)
list.add(13);
int num = list.get(0);
//컬렉션 선언시 자료형을 미리 정해서, 자료형이 어떤 것일지 찾을 필요없음
```

<br>

- 제네릭으로 자료형을 지정하면, 컬렉션에 다른 자료형 값이 저장되는 것을 컴파일 시 발견할 수 있음 *타입 세이프 기능

<br>
<br>

직접 만든 클래스에서 제네릭 사용 예시

GenericSample.class

```java

//<E>는 형식 매개변수. 자료형을 입력받아서 사용
public class GenericSample<E> {
    private E object;
    //E는 입력받은 자료형

    public E getObject(){
        return this.object;
    }
}
```

main.class
```java
GenericSample<String> generic = new GenericSample<String>();
//GenericSmapl.class E자리에 String 이 들어감. 클래스의 모든 E가 String으로 치환됨

String test = generic.getObject();
```
<br>
<br>

## 람다식
- 메서드를 간단히 기술하는 기법, 식별자 없이 실행 가능한 함수 표현식
- 인터페이스를 implements 안하고, 인터페이스 객체 생성하자마자 바로 구현
- 인터페이스 구현시, 클래스를 만들고, 메서드를 정의하고, 인스턴스로 만드는 과정을 간결하게 기술 가능
- ex)  (자료형 인수1, 인수2 ...) -> { 임의의 처리내용 }



InterfaceSample.class
```java
public interface InterfaceSample{
    abstract void sampleMethod(String name);
}
```
<br>

main.class
```java
InterfaceSample testlamabda = (String name) ->{
    System.out.println(name + "입니다.");
}

testlambda.sampleMethod("길동");

```

<br>
<br>

## 익명 클래스
- 프로그램의 문 중간에서 **클래스 형식으로 인터페이스 구현**

```java
public static void main(String[] args){
    InterfaceSample anonymous = new InterFaceSample(){
        //인터페이스 객체 생성과 동시에 처리함수 구현
        
        public void sampleMethod(String name){
            System.out.println(name + "입니다.");
        }
    };


    anonymous.sampleMethod("길동");
    //길동 입니다. 출력
}
```
