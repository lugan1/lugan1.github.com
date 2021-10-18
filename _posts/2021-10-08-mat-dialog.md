---
title: "[angular] matrial dialog 사용방법"
tags:
- log
- angular
categories:
- angular
date: '2021-10-08 09:16:00'
classes: wide
---

# 참조 및 참고 사이트 :  
[https://material.angular.io/components/dialog/examples](https://material.angular.io/components/dialog/examples)


# Material Dialog
1. App-module.ts 에 MatDialogModule 을 임포트한다.

2. 버튼을 사용하는 TS파일 생성자에 Matdialog 를 매개변수로 넣는다.
```javascript
constructor(public dialog: MatDialog) {

}
```
3. 다이얼로그 버튼을 띄우는 HTML 파일에서 버튼 클릭 이벤트를 지정한다.
4. 다이얼로그를 띄우는 버튼 클릭 이벤트를 TS 파일에서 구현
5. 버튼 클릭 이벤트 내용을 다음과 같이 구현
```javascript
this.dialog.open(다이얼로그 컴포넌트 클래스)
```

6. 여기서 방법이 나뉘어진다.
   - (1). 다이얼로그 컴포넌트 폴더를 아예 따로 만들어서 구현
   - (2). 다이얼로그 html 파일만 만들고, 버튼을 사용하는 TS파일에서 다음과 같이 추가
```javascript    
@Component({
  selector: 'dialog-elements-example-dialog',
  // 이 클래스 컴포넌트 이름으로 쓸 문자열

  templateUrl: 'dialog-elements-example-dialog.html',
  // 다이얼로그 템플릿 위치
})
export class DialogElementsExampleDialog {}
```

7. app-module.ts 에서 declarations 항목에 다이얼로그 컴포넌트를 추가한다.


<br/>

<br/>

8. 다이얼로그 템플릿을 작성한다

**dialog-elements-example-dialog.html**

```html
<h1 mat-dialog-title>Dialog with elements</h1>
<div mat-dialog-content>This dialog showcases the title, close, content and actions elements.</div>
<div mat-dialog-actions>
  <button mat-button mat-dialog-close>Close</button>
  
</div>
```

<br/>

# 다이얼로그에 데이터 전달하는 방법
1. 다이얼로그를 띄우는 메소드 매개변수에 \{ data : \{ key : value } } 를 추가한다.

```javascript
let dialogRef = dialog.open(YourDialog, \{
  data: \{ name: 'austin' },
});
```

2. 받는곳의 컴포넌트에서는 생성자에 다음과 같이 추가해서 데이터를 얻는다.
```javascript
export class YourDialog {
    
    name : string;
    
    constructor(@Inject(MAT_DIALOG_DATA) public data: \{name: string}) \{
        this.name = data.name;
   }
}
```

<br/>
<br/>

# 다이얼로그에서 데이터 받는 방법
전체 예제)

diloag 컴포넌트 HTML 파일
```html
<h1 mat-dialog-title>게시글 삭제 안내</h1>
<div mat-dialog-content>게시글을 정말 삭제 하시겠습니까? </div>
<div mat-dialog-actions>
  <!--mat-dialog-action 태그 안에 버튼 등록으로 다이얼로그 버튼 구현-->

  <button mat-button color="primary" [mat-dialog-close]="true">삭제</button>
  <!--버튼 클릭시 버튼 클릭이벤트도 따로 구현해야된다.-->
  <!-- 클릭이벤트 없이 데이터만 전달하고 싶은경우 [mat-dialog-close] 속성을 이용한다. -->

  <button mat-button mat-dialog-close color="primary" [mat-dialog-close]="false">취소</button>


  <!--<button mat-button mat-dialog-close color="primary">취소</button>-->
  <!-- mat-dialog-close 다이얼로그를 닫을때 쓰는 속성-->
</div>
```

dialog 컴포넌트 ts 파일
```javascript
import {Component} from "@angular/core";

@Component({
  selector:'delete-dialog',
  templateUrl:'post-delete-dialog.html'
})
export class DeleteDialog{
}
```

다이얼로그를 띄우는 컴포넌트 HTML 파일
```html
    <mat-card-footer class="mart_card_footer">
      <button class ="mat_raised_button" mat-raised-button color="primary" [routerLink]="['/BoardList']">목록</button>
      <button mat-raised-button color="primary">수정</button>
      <button mat-raised-button color="primary" (click)="openDeleteDialog()">삭제</button>
      <!-- 삭제 버튼 클릭시 DeleteDialog 컴포넌트를 띄운다-->
    </mat-card-footer>
```

<br/>

다이얼로그를 띄우는 컴포넌트 TS파일
```javascript
  openDeleteDialog():void{
    const dialogRef = this.dialog.open(DeleteDialog, { width: '300px', disableClose: true })
      .afterClosed()
      .subscribe(result =>{
        console.log(result);
    });

    //afterClose() 다이얼로그가 닫히면 Observable 객체를 반환 받는다.
    //subscribe() : observable 객체에 구독을 해놓아서 observable 객체가 반환받을때 실행된다. 즉 다이얼로그가 닫힐때 실행된다.
    //result : 다이얼로그의 HTML 파일에서 지정한 변수값을 얻어온다.
  }
  ```





