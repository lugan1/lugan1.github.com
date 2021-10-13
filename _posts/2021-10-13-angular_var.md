---
title: "[angular] 함수 매개변수 필수값 지정 안하는 방법. (변수?:자료형)"
tags:
- log
- angular
categories:
- angular
date: '2021-10-13 15:53:00'
classes: wide
---

# 함수 매개변수로 필수값 지정 안하는 방법
- 변수? : 자료형 문법 사용
- 변수 ?? '' 뜻
   - 변수값이 null 이면 ?? 뒤에있는 값을 value로 사용.
   - 즉, search 의 값이 null 이면 ''(공백) 값이 스트링에 들어간다.


예제)
```javascript
public getBoardList(page_limit : number, page_offset : number, search?: string) : Observable<ListResponse>{

    const options = {
      params: {
        page_limit,
        page_offset,
        search: search ?? ''
      },
    };

    return this.http.get<ListResponse>('/api/api/back/board/getBoardList', options);
    // page_limit , page_offset url 파라미터로 API 에 게시글 리스트를 조회한다.
  }
```


