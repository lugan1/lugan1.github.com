---
title: "[java] 멀티쓰레드 동기화, wait(), notify()"
tags:
- java
categories:
- java
date: '2021-09-23 02:52:57'
classes: wide
---

## 멀티 스레드의 동기화
- 멀티 스레드를 돌리면, 여러 스레드들끼리 서로의 작업에 영향을 미칠수 있음.
- 스레드들 간의 같이쓰는 변수, 같이쓰는 저장소 등등.. 한 스레드가 작업을 끝내지 않았는데 다른 스레드가 끼어들어와서 작업을 할수있음.
- 멀티 스레드를 하면서 스레드간에 영향을 미치지 않게 할려면 동기화 작업 필요

<br>
<br>

## 스레드의 동기화
- 스레드가 작업이 진행중일때 다른 스레드가 간섭하지 못하게 막는 것

- 동기화를 진행하려면 다른 스레드들의 접근을 막고싶은 코드를 임계영역(critical section)으로 지정함

- 한 스레드가 임계영역으로 지정한 코드 문장을 실행중이면, 그 코드가 끝나기 전까지 다른 스레드들이 접근을 못함 

- 임계영역으로 지정한 코드는 lock을 얻은 단 하나의 스레드만 접근 가능함 (객체 1개당 lock 1개)

- lock 이 없으면 임계영역 코드에 스레드가 접근 못함

<br>
<br>
<br>


## synchronized 키워드를 이용한 동기화 방법
### 1. 메서드 전체를 임계영역으로 지정하는 방법
- 메서드 앞에 synchronized 키워드를 붙이면 됨
- 임계 영역은 한번에 한 스레드만 접근 할수 있으니, 영역을 최소화 해야됨
- 임계 영역이 길 수록 성능이 떨어짐

```java
public synchronized void 메서드이름() {
    ...처리내용...
}
```

<br>
<br>

### 2. 코드의 특정 영역을 임계 영역으로 지정하는 방법
```java
synchronized (객체의 참조변수){
    ... 처리내용 ...
}
```

<br>
<br>

### synchronized 사용 예제)
```java
class Account{
    private int balance = 1000;
    //임계 영역 설정시 private 로 지정해줘야됨.
    //public 설정해서 다른 곳에서 직접 변수에 접근가능하면 동기화 의미가 없음

    public int getBalance() {
        return balance;
    }

    public synchronized void whithdraw(int money) {
        //출금 메서드, 메서드 임계영역 설정
        if (balance >= money) {
            //출금할려는 돈보다 통잔 잔고가 커야지 실행이 가능
            try { 
                Thread.sleep(100);
                }
            catch(InterruptException e){

                }
                balance = balance - money;
        }
    }
}


class RunnableTest implements Runnable {
    Account account = new Account();

    public void run() {
        while(account.getBalance() > 0){

            int money = (int) (Math.random() * 3 + 1) * 100;
            //100, 200, 300 중 임의로 랜덤으로 출금
            account.withdraw(money);
            system.out.println("balance : "+ account.getBalance()); 
        }
    }
}

class main {
    public static void mian(String[] args){
        Runnable runnable = new RunnableTest();
        new Thread(runnable).start();
        new Thread(runnable).start();
    }
}
```
<br/>
<br/>

실행결과
<br/>

(synchronized 키워드 없을때)
```bash
balacne : 900
balacne : 700
balacne : 600
balacne : 400
balacne : 200
balacne : -100
```

- 두 스레드가 한곳에 자원에 동시에 접근해서 -100 결과가 나옴

<br/>
<br/>

(synchronized 키워드 했을때)
```bash
balacne : 800
balacne : 500
balacne : 200
balacne : 0
balacne : 0
```

- 스레드간에 공유 코드에 임계영역 설정시 정상적으로 출력결과값이 나옴

<br/>
<br/>

### 스레드 동기화의 단점
- 동기화를 하면 데이터를 보호할 수는 있는데 한번에 한 스레드만 임계영역에 들어갈 수 있어서 비효율적임

- 데드락이 생길 수 있음. 한 스레드가 임계영역을 빠져나오지 못하면 다른 스레드는 영영 임계영역에 진입을 못하고 해당기달리게됨.

<br/>
<br/>

## wait() 와 notify()
- 스레드 동기화의 데드락을 해결가능하게 해줌

- 한 스레드가 임계영역을 사용중일때 특정구간에 wait를 걸어서 lock을 풀고 waitng pool 공간에 넣고, 해당 조건이 충족될때 notify 로 알려줘서 스레드를 깨움

- Object 클래스에 정의되어 있으며, 임계영역 블록내에서 사용가능

- wait() - 객체의 lock을 풀고 스레드를 해당 객체의 waitng pool에 넣는다.

- notify() - wating pool 에서 대기중인 스레드중에 하나를 깨운다. (순서는 없고, wating 대기중인 스레드들 중에 랜덤으로 아무거나 깨움)

- notifyall() - wating pool 에서 대기중인 모든 스레드를 깨운다.

<br/>
<br/>

### wait() notify() 사용예제
```java
class Account {
    int balance = 1000;

    public synchronized void withdraw(int money) {
        //출금 메소드
        while(balance < money) {
            //만약 통장 잔고가 출금 머니보다 적으면, lock을 풀고 wating

            try {
                wait(); //작업중인 스레드가 lock 을 풀고 wating pool 에서 기다림
                } catch (interruptedException e){}
            }
        balance = balance - money;
    }

    public synchronized void deposit(int money) {
        //입금 메소드
        balance = balance + money;
        notify(); //wating pool 에서 대기중인 스레드를 깨움
    }
}
```

<br/>
<br/>

## wait(), notify() 단점

- **wait(), notify() 는 어떤 스레드를 재우고, wating pool에서 어떤 스레드를 깨울지 그 대상이 불분명함**

- lock, awake 대상의 불분명함을 해소하기 위해 나온것이 Lock & Condtion