---
title: "[github pages] minimal_mistakes 커스텀 스킨하는법"
tags:
- jekyll
- VScode
- scss
- minimal_mistakes
categories:
- github pages
---

minimal mistakes 테마를 사용하고 있는데 contrast 스킨을 사용하면 포스트 제목이 파란색으로 뜨는게 마음에 안들어서, 

어떻게 포스트 제목 색깔만 따로 변경할수 없나 하고 찾아보았다.

![contrast](/assets/image/posts_image/post_cumtomskin/contrast.png)



찾아본 결과 **sass->minal_takes->skins** 폴더에 skin들 파일이 들어있고 텍스트 편집기로 값을 수정하면 되는거였다.

(나는 VScode로 열어서 수정했다.)

![path](/assets/image/posts_image/post_cumtomskin/path.png)
![air](/assets/image/posts_image/post_cumtomskin/air.png)


이참에 커스텀 스킨을 만들수도 있다. 양식을 복사해서 새롭게 skins 폴더에 scss 파일을 만든 다음에  **config.yml** 파일에서 skin 항목에 새롭게 커스텀한 skin 파일 이름을 적어주면 적용이 된다.

![config](/assets/image/posts_image/post_cumtomskin/config.png)
