---
title: '스크롤 값으로 opacity 값 비율구하기'
excerpt: '특정 영역내에서 스크롤 시 opacity 값을 바꿔 나타났다 사라지게 하는 방법을 알아보겠습니다.' 
categories: [JavaScript]
tags: [자바스크립트 스크롤 opacity]
last_modified_at: 2021-02-07T01:18:00-19:00
toc: true 
toc_label: '목차'
sitemap :
changefreq : daily
priority : 1.0
---

> 스크롤 값에 따라 opacity 값을 할당하여 자연스럽게 나타나거나 사라지게 하는 방법을 알아보겠습니다. <br>

## 섹션 내에서의 opacity 값 비율 구하기 

<img src='/assets/images/allScrollSection.png' alt='profile' style="width:700px; margin-top:15px; margin-bottom:15px; box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px, rgba(0, 0, 0, 0.024) 0px -6px 16px -6px;"/>


만약 위와 같이 4개의 섹션이 존재하고, **section 2**에서 스크롤 위치 값을 이용해서 opacity 값을 구하는데 <br>
**section 2**가 시작될때 opacity값이 0에서부터 점점 증가하여 끝날때쯤 opacity 값이 1이되게끔 하려면 어떻게 해야할까요?? 

### 섹션 2번 내에서의 비율 구하기

범위가 0~1인 `opacity` 값을 섹션의 높이와 스크롤 위치를 이용해서 구하는 방법 입니다.

<img src='/assets/images/scrollSectionTwo.png' alt='profile' style="width:700px; margin-top:15px; margin-bottom:15px; box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px, rgba(0, 0, 0, 0.024) 0px -6px 16px -6px;"/>

위의 그림은 **section 2**를 확대한 것으로 4개의 부분으로 나누어 애니매이션을 수행하도록 합니다.

**section 2**에서 스크롤 값에 따라 `opacity` 값을 조절하여 html 요소를 나타나게 하거나 사라지게 할려면 opacity 값은 0 ~ 1 값으로 나와야 합니다.<br>

- 그림에서 <span style="color:purple">0</span>과 <span style="color:purple">1</span>은 `opacity`의 값 범위입니다.

- partScrollStart : 이 지점부터 opacity값이 0에서부터 증가합니다. 
  ```js
  const partScrollStart = 0.1 * scrollHeight;
  ```
- partScrollEnd : 이 지점까지 해서 opacity값이 1이 됩니다.
  ```js
  const partScrollEnd = 0.2 * scrollHeight;
  ```
- partScrollHeight : start와 end의까지의 높이
  ```js
  const partScrollHeight = partScrollEnd - partScrollStart;
  ```

- start지점부터 end지점까지의 스크롤 위치에 따른 opacity 값 반환
  ```js
  let opacityValue = ( currentYOffset - partScrollStart ) / partScrollHeight * ( 1 - 0 ) + 0;
  ```


---

**참고** <br>
