---
title: "[gitLab] git work flow 전략"
tags:
- log
- git
categories:
- git
date: '2021-10-04 21:42:00'
classes: wide
---
# 출저 및 참고 사이트  
[https://medium.com/extales/git%EC%9D%84-%EB%8B%A4%EB%A3%A8%EB%8A%94-workflow-gitflow-github-flow-gitlab-flow-849d4e4104d9](https://medium.com/extales/git%EC%9D%84-%EB%8B%A4%EB%A3%A8%EB%8A%94-workflow-gitflow-github-flow-gitlab-flow-849d4e4104d9)  
[https://nomad-programmer.tistory.com/39](https://nomad-programmer.tistory.com/39)  

<br/>
<br/>

# Git Work Flow 전략
- **git flow 전략**
- **github flow 전략**
- **gitlab flow 전략**

<br/>

## Git Flow 전략
- 가장 최초로 제안된, 플로우
- 브렌치 전략에 있어서 다른 워크플로우들보다 엄격하다.
- git flow 는 다음과 같은 5가지의 브렌치를 규정하고있다.
   - Master
   - Develop
   - Feature
   - Release
   - Hotfix

### **Master**
- 릴리즈를 할 때 사용하는 최종 단계의 메인 브랜치다.
- Master브랜치는 릴리즈 기록을 담고 있다.
- 태그를 통해 버젼잉(versioning)을 하게 된다.

### **Develop**
- 다음 릴리즈 버전 개발을 진행하는 브랜치다.
- 어떤 기능의 구현이 필요해지면 Develop브랜치에서 다시 브랜치를 내어 개발을 진행하며, 개발이 완료된 기능은 다시 Develop브랜치로 병합된다.

### **Feature**
- Develop브랜치에서 기능 구현을 이유로 브랜치를 낼 때, 이 브랜치가 Feature브랜치다.
- 즉 Devleop 의 각각의  세부 브렌치다.
- 브랜치를 내는 기준은 한 기능 단위가 된다.

### **Release**
- Develop브랜치에서 파생되는 브랜치다.
- 현재 코드가 Master브랜치로 병합될 수 있는지 테스트를 하고 테스트 과정에서 발생한 버그를 고치는 역할을 담당하고 있다.
- 이상이 없다면 Release브랜치는 Master브랜치로 병합된다.

### **Hotfix**
- 검수를 진행했음에도 릴리즈된 Master브랜치에서 버그가 발견될 수 있다.
- 이때 Master브랜치에서 Hotfix브랜치를 내어 버그를 수정한다.
- 디버그가 완료되었다면 Master브랜치와 Develop브랜치에 병합해주고 브랜치를 닫는다.

<br/>
<br/>

![git_flow.png](/assets\image\posts_image\post_git_flow\git_flow.png)


<br/>

### **Git Flow 전략 단점**
- 각각의 브랜치들이 너무 많고, 복잡하며, 규칙이 엄격하여 생산성을 떨어트릴 수 있다.


<br/>
<br/>

## Github Flow 전략

<br/>

![github_flow.png](/assets\image\posts_image\post_git_flow\github_flow.png)




- Github Flow는 다음과 같은 3개의 브렌치만 사용한다.
   - Master
   - Bugfix
   - Feature

- Github flow는 Master브랜치가 릴리즈에 있어서 절대적인 역할을 한다.
- Master브랜치는 항상 최신 버전을 유지한다. 그리고 무조건적으로 stable한 상태를 담보한다.
- Develop브랜치가 존재하지 않고 Feature브랜치는 Master브랜치에서 생성되며,병합된다.
- 병합을 할 때는 무조건 <u>**pull request**</u>를 하여 코드에 대한 검토를 받도록 한다.
- Github flow는 CI가 필수적이다.

**pull request**
- 수정 완료한 코드가 있으니 자신의 branch를 가져가서 검토후에 병합해 달라고 요청하는것
- psuh 권한이 없는 오픈 소스 프로젝트에 기여할 때 많이 사용된다.

<br/>
<br/>
<br/>

## Gitlab Flow 전략
<br/>

![gitlab_flow.png](/assets\image\posts_image\post_git_flow\gitlab_flow.png)

<br/>

- Gitlab flow는 너무 단순해진 Github flow에 보완하는 내용을 가미하여 제안된 방식이다.
- Gitlab flow는 다음과 같은 브렌치를 사용한다
   - Master
   - Production
   - Pre-Production

- Gitlab flow의 Production 브렌치는 Gitflow의 Master브랜치역할과 같다.
- Gitlab flow의 Master브랜치는 Production 브랜치로 병합한다.
- 이렇게 브랜치전략을 가져갈 때의 이점은 Production브랜치에서 릴리즈된 코드가 항상 프로젝트의 최신버전 상태를 유지해야할 필요가 없다는 것이다.

<br/>
<br/>

## Gitlab Flow 추가 설명
출저 및 참고 사이트 :  
[https://nomad-programmer.tistory.com/39](https://nomad-programmer.tistory.com/39)  

- feature 브랜치의 작업 결과가 master 브랜치로 병합된다
- 배포 준비가 되면 master 브랜치에서 production 브랜치로 병합한다.
- Production 브랜치는 오직 배포만을 담당한다.
- 즉, Production 브랜치 = Release(배포) 브랜치 이다.

<br/>
<br/>

## Pre-production 브랜치 추가
- Pre-Production 브랜치는 테스트 브랜치 이다.
- 개발 환경에서 바로 배포하지 않고, 사용 환경과 동일한 테스트 환경에서 코드를 테스트 하는 것이다.
- 즉, pre-production 브랜치에서 런칭 환경 테스트를 먼저하고, 이상이 없으면 production 브랜치에 배포하는 형태이다.
- 웹개발에서 예를 들자면, 로컬 저장소에서 기능 개발을 한 다음, 테스트 서버(pre-production)에서 시험하고, 실제 서비스로 배포하는 것을 production 브랜치에 병합 하는 것으로 생각하면 된다.