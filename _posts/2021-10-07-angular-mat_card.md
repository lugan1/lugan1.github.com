---
title: "[angular] mat-card , mat-list"
tags:
- log
- angular
categories:
- angular
date: '2021-10-07 11:42:00'
classes: wide
---

# \<mat-card>
- 단일 주제의 컨텍스트에서 텍스트, 사진 및 작업을 위한 콘텐츠 컨테이너다.
- 중요. **컨텐츠 콘테이너**

<br/>

## 기본적인 카드 섹션들
|요소|설명|
|---|---|
|\<mat-card-title>|카드 제목|
|\<mat-card-subtitle>|카드 부제목|
|\<mat-card-content>|카드 안에 다음 내용들|
|\<img mat-card-image>|카드 이미지를 사용할때 쓴다, 이미지를 컨테이너 너비로 늘린다.|
|\<mat-card-actions>|카드 하단의 버튼용 컨테이너|
|\<mat-card-footer>|카드 하단에 고정된 섹션을 사용할때 쓴다.|

<br/>

## \<mat-card-header>로 카드에 풍부한 헤더를 추가 할 수 있다.
- 이 헤더에는 다음과 같은 요소가 포함될수 있다.
- \<mat-card-title> : 헤더 내의 제목
- \<mat-card-subtitle> : 헤더 내의 부제목
- \<img mat-card-avatar> : 헤더 내에서 아바타로 사용되는 이미지

<br/>
<br/>

# mat-list
- 리스트를 표시할때 사용

예제)

![mat-list.png](/assets\image\posts_image\mat-list.png)

<br/>

소스코드)  
**html 파일**
```html
<mat-list>
  <div mat-subheader>Folders</div>
  <mat-list-item *ngFor="let folder of folders">
    <mat-icon mat-list-icon>folder</mat-icon>
    <div mat-line>{{folder.name}}</div>
    <div mat-line> {{folder.updated | date}} </div>
  </mat-list-item>
  <mat-divider></mat-divider>
  <div mat-subheader>Notes</div>
  <mat-list-item *ngFor="let note of notes">
    <mat-icon mat-list-icon>note</mat-icon>
    <div mat-line>{{note.name}}</div>
    <div mat-line> {{note.updated | date}} </div>
  </mat-list-item>
</mat-list>


<!-- Copyright 2021 Google LLC. All Rights Reserved.
    Use of this source code is governed by an MIT-style license that
    can be found in the LICENSE file at http://angular.io/license -->
```

**TS파일**
```javascript
import {Component} from '@angular/core';

export interface Section {
  name: string;
  updated: Date;
}

/**
 * @title List with sections
 */
@Component({
  selector: 'list-sections-example',
  styleUrls: ['list-sections-example.css'],
  templateUrl: 'list-sections-example.html',
})
export class ListSectionsExample {
  folders: Section[] = [
    {
      name: 'Photos',
      updated: new Date('1/1/16'),
    },
    {
      name: 'Recipes',
      updated: new Date('1/17/16'),
    },
    {
      name: 'Work',
      updated: new Date('1/28/16'),
    }
  ];
  notes: Section[] = [
    {
      name: 'Vacation Itinerary',
      updated: new Date('2/20/16'),
    },
    {
      name: 'Kitchen Remodel',
      updated: new Date('1/18/16'),
    }
  ];
}


/**  Copyright 2021 Google LLC. All Rights Reserved.
    Use of this source code is governed by an MIT-style license that
    can be found in the LICENSE file at http://angular.io/license */
```