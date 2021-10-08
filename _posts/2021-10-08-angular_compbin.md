---
title: "[angular] component 이동 후에 데이터 전달방법"
tags:
- log
- angular
categories:
- angular
date: '2021-10-08 17:54:00'
classes: wide
---

# component 이동후에 데이터도 같이 전달하는 방법
- click 이벤트에 다음과 같이 작성
```javascript
  navigate_modify(): void{
    this.router.navigateByUrl('/BoardList/modify/'+this.postIdx, {state: this.board})
  }
```

# 받는쪽에서 history.state 로 받는다.
```javascript
  ngOnInit(): void {
    this.board = history.state
    console.log(this.board?.title)
  }
```

