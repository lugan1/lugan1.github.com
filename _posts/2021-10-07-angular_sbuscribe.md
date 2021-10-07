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
- 옵저버블을 활용해서 비동기 프로그래밍, 즉 데이터스트림과 데이터의 변화를 감지한다.
- 모든 이벤트를 observable로 추상화 하여 시간에 따른 스트림으로 간주할 수 있게한다.
- 그리고 각 이벤트가 observer(이벤트핸들러)에게 전달되기 전에 map, filter 등의 operator를 이용해 이벤트를 필요한 형태로 재가공하여 oberver 에게 전달할 수 있다.
- observable 에서 발생한 이벤트가 observer 에게 전달되기 전에 여러가지 operator 들을 이용하여 이벤트를 보다 선언적으로(직관적으로) 처리 할 수 있도록 해준다.

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

# Subscirbe
- 내가 바라보고있는 주제에 대해서 어떠한 이벤트가 발생함에 따라서 그 행위를 처리하는 함수
- 구독을 시작하게된 행위는 변경된 이벤트에 대해서 계속 반응하게 된다.
- 즉, 한번 구독(Subscribe)을 시작하면 따로 중지를 시키지 않으면 계속 구독을 하게 된다.

- Rxjs 에서 Subscribe를 실행하면 Subscription 이라는 객체를 돌려준다.
- 해당 객체에는 현재 구독중인 상태 및 중지를 할 수 있는 기능(unsubscribe)가 존재한다.
