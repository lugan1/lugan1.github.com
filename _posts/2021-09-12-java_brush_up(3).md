---
title: "[java 복습(3)] 배열, 컬렉션, 이터레이터, 스레드"
tags:
- java
categories:
- java
date: '2021-09-12 23:03:57 +0900'
classes: wide
last_modified_at: '2021-09-13 03:10:01 +0900'
---

## 배열
- 자료형[ ] 배열명 = new 자료형[크기];

<br>배열 예시)
```java
String[] name = new String[30];
```

## 컬렉션
- 객체의 집합을 모아서 관리하는 데이터 구조

    1. **List** : 크기가 동적 할당이 가능한 배열
    2. **Set** : 순서 없음, 중복허용 x (집합)
    3. **Map** : 
    - 키와 값이 쌍으로 저장되는 컬렉션
    - 키는 중복값이 될 수 없음
    - 데이터 추출시 키를 지정해서 대응하는 값을 가져옴

List 종류
<br>
1. Array List  : 크기를 나중에 변경 할 수 있는 배열
2. Linked List : 요소 추가와 삭제를 빠르게 할 수 있는 리스트

Array List 선언
```java
List<E> 변수명 = new ArrayList<E>();
//E -> 자료형, 형생략 가능(제네릭)
```
<br>

Array List 메소드
<br>

|메소드명|내용|
|-----|------|
|boolean add(E e)|끝에 요소추가|
|void add(Int index, E element)|지정한 위치에 요소추가|
|E set(Int index, E element)|지정한 위치의 요소값 변경|
|E get(Int index)|지정한 위치의 요소값 가져옴|
|boolean remove(Int index)|지정한 위치의 요소값 삭제|
|void clear()|전부 삭제|
|boolean isEmpty()|요소가 없으면 true 반환|
|int size()|요소의 갯수 반환|

<br>
<br>

## 이터레이터
- boolean hasNext() : 다음 요소가 있으면 true 반환
- object next() : 다음 요소 추출
```java
Iterater<String> itertest = list.iterator();
itertest.hasNext();
//다음 요소가 있는지 확인
```

<br>

## 스레드
- 프로세스 내에서 실행되는 흐름의 단위

![thread1](/assets/image/posts_image/thread1.png)

<br>

- 프로세스 내의 스레드들은 메모리를 공유한다.
- 동시에 여러작업을 할때, 멀티 프로세스보다 멀티 스레드가 시스템 자원을 더 적게 사용한다.
- 스레드의 경우, 공유 자원에 대한 동기화(Syncronize) 이슈가 발생함.
- 스레드간의 통신은 공유 메모리(Heap 영역)을 통해 가능하다.
- 프로세스간의 통신은 IPC등의 기술을 사용해야 서로 통신가능

<br>

사용방법
1. 클래스에 Runnable 을 implements 한다.
2. 생성자를 만든다.
3. run 메소드를 구현한다.
(준비 끝.)


4. 클래스 객체를 생성한다.
5. Thread 객체를 생성한다.
6. 생성한 Thread 객체 인수에 implements Runnable 했던 클래스 객체를 집어넣는다.
7. thread객체.start(); 로 스레드 실행 

<br>

```java
public class MultiThreadSample implemnets Runnable{

    public MutiThreadSample(){
    }
    //생성자 만듬


    public void run(){
        처리내용
    }
    // Runnable 을 implements 하고, run 메소드를 구현해줘야 함.

    public static void main(String[] args){
            MutiThreadSample mutiThreadSample = new MultiThreadSample();
            //runnable implemnts, run() 메소드 구현한 클래스 객체 생성후

            Thread thread1 = new Thread(mutiThreadSample);
            //Thread 객체 생성시 매개변수에 집어넣어서

            thread1.start(); 
            //thread 객체.start(); 으로 스레드 시작
    }
}
```

<br>
<br>

## 스레드 풀(Thread Pool)
- Java 에서는 스레드풀 이라는 기능을 제공함
- 사용할 스레드를 제한된 수 만큼 만들어두고, 일정한 규칙에 따라 실행하는 기능

- java.util.concurrent.* 패키지에서 사용가능

스레드 풀 기능을 제공하는 인터페이스
<br>

|인터페이스|설명|
|---------|----|
|ExcutorService|스레드 수를 제한|
|ScheduledExcutorService|일정시간 후에 스레드 시작|

- import java.util.concurrent.ExcutorServices;
- import java.util.concurrent.Excutor;

등으로 임포트 해서 사용

<br>
<br>

Executor 클래스의 주요 메서드

|인터페이스|설명|
|---------|----|
|newSingleThreadExecutor|싱글 스레드로 동작하는 Executor인스턴스 반환|
|newFixedThreadPool|지정한 최대 동시 실행 스레드 수로, ExecutorService의 인스턴스 반환|
|newScheduledThreadPool|지정한 최대 동시 실행 스레드 수로, ScheduledExecutorService의 인스턴스를 반환|

<br>
<br>

```java
ExecutorService executorService = Executors.newFixedThreadPool(3);
// 스레드 동시 실행수는 3, 매개변수를 1로 설정시에는 하나씩 차례대로 실행

executorService.execute(쓰레드1);
.
.
.
executorService.execute(쓰레드3);
executorService.shutdown();
// 스레드는 execute() 메서드로 시작하고, shutdown() 메서드로 종료.
// shutdownNoew() 메서드 사용시 즉시 종료

try{
            // 타임아웃 후에도 아직 실행이 끝나지 않으면
    if (!executorSErvice.awaitTerminaton(5, TimeUnit.MINUTES)){
        // awaitTermination(시간, TimeUnit.MINUTES)
        // 시간 경과하면 false 반환.



        executorSErvice.shutdown();
        // 즉시 종료

    }
} catch (InterruptedExcetion e){
    //종료 대기 시에 오류가 발생시

    e.printStackTrace();
    executorService.shutdownNow();
    // 즉시 종료
}
```

## 스레드 세이프
- 멀티 스레드 프로그램에서는 복수의 스레드가 인스턴스를 공유할 가능성이 있음

- 멀티 스레드로 동작하는 프로그램에서 복수의 스레드로부터 호출되더라도 기대대로 동작하는 것

<br>
<br>

스레드 세이프 방법 (Synchronized 사용)
1. 스레드마다 인스턴스를 생성
2. Syncronized를 사용
```java
Syncronized (배타제어 대상) {
    //배타제어 대상-> 락을 걸 오브젝트

    코드
}
```

- Atomic ~ 클래스 사용시에도 스레드 세이프 기능 있음
