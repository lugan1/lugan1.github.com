---
title: "[angular] Rxjs , Subscribe"
tags:
- log
- angular
- typescript
categories:
- angular
date: '2021-10-07 10:07:00'
classes: wide
---

# 참고 및 예제 사이트 :  
[https://min9nim.vercel.app/2020-04-24-rxjs/](https://min9nim.vercel.app/2020-04-24-rxjs/)


# RxJS (Reactive Extentions for JavaScript)
- Rx 패턴을 사용하는 javascript
- Rxjava, rxCotlin, 등등이 있다.

- 옵저버블을 활용해서 비동기 프로그래밍, 즉 데이터스트림과 데이터의 변화를 감지한다.
- 모든 이벤트를 observable로 추상화 하여 시간에 따른 스트림으로 간주할 수 있게한다.
- 그리고 각 이벤트가 observer(이벤트핸들러)에게 전달되기 전에 map, filter 등의 operator를 이용해 이벤트를 필요한 형태로 재가공하여 oberver 에게 전달할 수 있다.
- observable 에서 발생한 이벤트가 observer 에게 전달되기 전에 여러가지 operator 들을 이용하여 이벤트를 보다 선언적으로(직관적으로) 처리 할 수 있도록 해준다.

<br/>

# RxJS의 이벤트 처리 방식 예제
## 일반적인 이벤트 처리 방식
```javascript
document.addEventListener('click', () => console.log('Clicked!'))
```

<br/>

## RxJS를 이용한 이벤트 처리 방식
```javascript
import {fromEvent} from 'rxjs'

const observable = fromEvent(document, 'click')
const observer = () => console.log('Clicked!')
observable.subscribe(observer)
```

### 1. fromEvent를 이용해서 이벤트를 observable 객체로 만든다.
### 2. observer 변수로 클릭이벤트를 구현한다. / observer(이벤트핸들러) 를 정의한다.
### 3. observable이 클릭 이벤트를 등록(구독)한다 / observable 이 observer 을 구독한다.
### * Subscribe : 이벤트 / 함수를 객체에 등록하는 행위인듯

<br/>
<br/>
<br/>

## 일반적인 이벤트 클릭 예제(클릭한 횟수를 매번 표시)
```javascript
let count = 0
document.addEventListener('click', () => console.log(`Clicked ${++count} times`))
```

## RxJS를 이용한 이벤트 클릭 예제 (클릭 횟수 표시)
```javascript
import {fromEvent} from 'rxjs'
import {scan} from 'rxjs/operators'

const observable = fromEvent(document, 'click').pipe(scan(count => count + 1, 0))
const observer = count => console.log(`Clicked ${count} times`)
observable.subscribe(observer)
```

### 1. observable을 정의한다.
- 어떤 이벤트들을 하나의 observable로 묶을 것인가
- 적절한 operator 를 이용하여 observable 을 가공

### 2. observer 정의
- observable 로 부터 이벤트를 전달받으면 어떻게 처리할 지를 정의

### 3. observable 과 observer 를 연결
- oserver 와 observable 을 연결한다 (**observable.subscribe()**)


<br/>
<br/>

# Observable
- value가 바뀐다던지 어떤 값이 바뀔때마다 메소드(이벤트)를 발생시킨다. subscribe() 메소드로 그 이벤트내용을 처리할수 있다.

- 시간 흐름에 따라 발생하는 이벤트들의 집합이다.
- 단순하게 이벤트 스트림으로서 생각해 볼 수 있다.
- observable을 구독시에 observer 객체로 next, error, complete 3가지 핸들러를 쓸수있다.
- observable은 이벤트를 동기 또는 비동기로 발생 시킬수 있다.

## observable.next()
- 길다란 파이프 입구 안으로 매개변수를 집어 넣는다고 생각하면 된다.

- 매개변수를 받는 쪽은 subscribe() 를 구현해 받은 매개변수를 처리해줘야 한다.


<br/>
<br/>

# Subscirbe
- 콜백이나, promise 로 이벤트 처리를 하는것은 1회성이다. 하지만 Subscribe를 통해 밸류 체인지 이벤트를 처리하면 제한없이 이벤트를 실행할수 있다. 그것이 바로 구독이다.
- 옵져버블객체.subscribe() 를 하면, 옵져버블의 값이 바뀔때마다 Subscribe { } 블록안의 처리코드가 실행된다. 구독취소를 하지 않는한 제한없이 실행된다.



- 내가 바라보고있는 주제에 대해서 어떠한 이벤트가 발생함에 따라서 그 행위를 처리하는 함수
- 구독을 시작하게된 행위는 변경된 이벤트에 대해서 계속 반응하게 된다.
- 즉, 한번 구독(Subscribe)을 시작하면 따로 중지를 시키지 않으면 계속 구독을 하게 된다.

- Rxjs 에서 Subscribe를 실행하면 Subscription 이라는 객체를 돌려준다.
- 해당 객체에는 현재 구독중인 상태 및 중지를 할 수 있는 기능(unsubscribe)가 존재한다.

- observable 을 구독하면(subscribe) subscription 객체가 리턴된다.
- subscription 객체를 이용해 해당 구독을 취소 할 수 있다.
- subscription 은 구독을 취소하기 위한 용도로서만 사용된다.

<br/>

## 연쇄적인 Subscribe
- subscribe 안에 또다른 observable 값을 바꿔서 체인지 이벤트 발생, 다른 곳에서 subscribe 로 그 이벤트를 처리. 즉 연쇄적으로 subscribe가 발생하는 것

<br/>

**연쇄적인 Subscribe 예제 )**
```javascript
    this.sub = this.form.valueChanges.subscribe(value => {
      this.boardService.somethingUpdated.next(value.search);
      // next( ) : 파이프 입구 안으로 데이터를 밀어 넣는다고 생각하면 된다. 받는쪽은 subscribe를 구현해 데이터를 처리해줘야 한다.
    });

    this.boardService.somethingUpdated.pipe(
      distinctUntilChanged(),
      debounceTime(1000)
      // 1초씩 딜레이를 주어서 트래픽을 낮춘다.

    ).subscribe(searchText => {
      this.searchText = searchText;
      this.reload(searchText);
      // HTTP 통신은 1회 통신후 일방적으로 unsubscribe 를 하는데, 재 통신 필요할때마다 subscribe를 다시 해줘야 한다.
      // reload() : observable 객체를 다시 usbscirbe 하는 메소드

    });
  }

  reload(search: string) {
    this.boardService.getBoardList(search)
      .subscribe(value => this.dataSource_test.data = value)
  }
```

<br/>

### **Observable.next()**
- 파이프 입구안으로 데이터를 넣는다고 생각하면 된다.
- 주로 TS파일 끼리의 데이터를 전달할때 사용
- 받는쪽은 subscribe 를 구현해 데이터를 처리해줘야 한다.

<br/>
<br/>

# Subject
- 멀티캐스트를 위한 특별한 유형의 Observable 이다.
- 일반적으로는 하나의 observable 에는 하나의 observer 만 등록할 수 있다.
- 하지만, Subject 를 이용하면 하나의 observable 을 구독하는 여러개의 observer 를 생성하고 등록할 수 있다.
- Subject 는 observable 이지만 observer 로서 또 다른 observable 을 구독할 수 있다.


![angular.subject.png](/assets\image\posts_image\angular_subject.png)

- 여러 컴포넌트에서 비동기적으로 observable 객체에 대한 subscribe 를 할때 사용한다.