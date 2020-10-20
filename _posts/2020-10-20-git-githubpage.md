---
title: 'Github Page로 웹 호스팅'
excerpt: '자바스크립트 공부하면서 복습겸 순수 자바스크립트만을 이용하여 To Do List(할 일 목록)를 만들어 보았습니다.'
categories: [Git]
tags: [Github Page]
last_modified_at: 2020-10-20T01:15:00-16:00
toc: true
toc_label: '목차'
---
## 깃허브 페이지로 웹 호스팅 하기

간단하게 Github Page를 이용해서해서 웹 무료 호스팅을 해보도록 하겠습니다.

### REPOSITORY 생성
repository를 생성하고 Repository name을 지정합니다. <br>
저는 "test_project"로 이름을 지정했습니다. <br>
지정한 Repository name이 깃허브 주소로 `https://chanho-yoon.github.io/{Repository name}` 설정됩니다. (한글x)

<img src='/assets/images/githubpageCreate.png' alt='profile' style="width:600px; margin-top:15px; margin-bottom:15px; box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px, rgba(0, 0, 0, 0.024) 0px -6px 16px -6px;"/>

### GIT INIT
호스팅을 할 프로젝트 폴더로 들어가 git 저장소를 생성한 뒤 `commit` -> `push` 합니다. <br><br>
<strong><span style="color:red">주의사항</span></strong>
- 반드시 파일 이름이 `index.html`로 프로젝트 폴더내에 파일이 존재해야합니다.

```
git init
git add .
git commit -m "fisrt commit"
git remote add origin https://github.com/chanho-Yoon/test_project.git
git push origin master
```

### GH-PAGES
`gh-pages` 브랜치를 생성하고 원격 저장소로 branch를 push 합니다.
<strong><span style="color:red">주의사항</span></strong>
- 브랜치명은 반드시 `gh-pages`로 생성해야 합니다.

```
git checkout -b gh-pages
git push origin gh-pages
```

### 확인
오류 없이 진행이 다 되었다면 해당하는 프로젝트의 repository의 Settings에서 Github Pages 목록 처음 부분에 웹호스팅된 주소와 Source 부분의 
branch가 `gh-pages`로 되어 있는 것을 볼 수 있습니다.

<img src='/assets/images/githubpageCheck.png' alt='profile' style="width:600px; margin-top:15px; margin-bottom:15px; box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px, rgba(0, 0, 0, 0.024) 0px -6px 16px -6px;"/>

간혹 바로 반영이 안될 때가 있습니다. 이러할 경우 몇 분 정도 기다렸다가 들어가시면 정상적으로 접속됩니다.

---

**참고**

>
