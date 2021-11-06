---
title: "[angular] HTML 템플릿에 Paginate 속성 쓸시에 Unsolved Pipe paginate 해결방법"
classes : wide
tags:
- angular
- error
categories:
- angular
date: '2021-10-12 14:36:00'
---

# 서론
- ngx-Paginate를 npm 인스톨로 설치하고, app-modules 에 추가 한 다음에, 템플릿에 \<li *ngFor="let item of boardList | paginate : { itemsPerPage: 10, currentPage: page}"></li> 를 했는데 paginate 에 빨간줄이 쳐지면서 unsolved pipe paginate 오류가 뜨는 것이었다.

# 해결방법
- CTRL + SHIFT + A 눌러서 Registry 입력 -> angular.enablevyMatadataSuppoert 체크해제

- app-modules 에서 ngx-eidtor 가 import 가 안되어 옵션을 체크했는데, 반대로 템플릿에서 ngx-paginate 가 안먹힌다.

- 이방법을 쓰면 대신, ngx-editor 가 app-modules 에서 import 가 안된다.

- 다른 방법을 찾아보아야 겠다.

- app-modules 에서 NgxEditorModule 이 빨간줄을 띄우지만, 런타임을 돌려보면, 정상적으로 실행되고 보여진다.