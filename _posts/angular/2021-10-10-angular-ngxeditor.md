---
title: "[angular] ngx-editor 적용방법 (텍스트 에디터)"
tags:
- log
- angular
categories:
- angular
date: '2021-10-10 19:18:00'
classes: wide
---

# ngx-editor 설치 및 import
## npm 명령어로 다음과 같이 입력한다.
- npm install ngx-editor --save

## app-moduels.ts 에 다음과 같이 import 추가한다.
```javascript
imports : [ 
    NgxEditorModule 
    ]
```


# HTML 파일에 다음과 같이 사용된다
```html
            <div class="NgxEditor__Wrapper">
              <ngx-editor-menu [editor]="editor"> </ngx-editor-menu>
              <ngx-editor
                formControlName="content"
                [editor]="editor"
                [ngModel]="board.content"
                [disabled]="false"
                [placeholder]="'Type here...'"></ngx-editor>
            </div>
```

<br/>

# TS 파일에 다음과 같이 추가한다
```javascript
editor!: Editor;
// 변수명! -> typescript 의 엄격한 검사로 인해 undifined 를 안쓰면 빨간줄 뜨는데, 변수명! 를 하면 해결된다.

  ngOnInit(): void {
    this.editor = new Editor();
  }


  // make sure to destory the editor
  ngOnDestroy(): void {
    this.editor.destroy();
  }


```