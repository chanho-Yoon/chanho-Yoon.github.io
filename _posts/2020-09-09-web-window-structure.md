---
layout: post
title: 'Browser 구조'
excerpt: 'Browser 구조에 대해 공부하겠습니다.'
categories: [Web]
tags: [Browser structure,브라우저 구조]
last_modified_at: 2020-09-09T01:15:00-16:00
toc: true
toc_label: '목차'
sitemap :
changefreq : daily
priority : 1.0
---

## 1. Browser 구조

<img src='/assets/images/browserStructure.png' alt='profile' style="width:600px; margin-top:15px; margin-bottom:15px; box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px, rgba(0, 0, 0, 0.024) 0px -6px 16px -6px;"/>
<br>

## 2. Window 객체

우리가 인터넷 브라우저를 열게 되면 **Window**라는 전체적인 오브젝트가 있고 그 안에 **DOM,BOM,JavaScript**가 존재합니다.<br>
이러한 모든 객체를 포함하고 있는 객체가 Window 객체 입니다.<br>
브라우저의 콘솔창(맥 단축키: cmd + option + i)에 들어가 `console.log(window)`하면 window에 관련된 다양한 함수와 오브젝트들을 확인할 수 있습니다.

## 3. Window 객체가 포함하는 객체

### 3.1 DOM(Document Object Model)

DOM은 웹페이지의 문서를 제어하는 객체입니다. <br>
웹 페이지는 일종의 **문서(document)** 입니다. DOM은 웹 페에지의 객체 지향 표현이고 자바스크립트와 같은 스크립팅 언어를 사용해서 DOM을 제어할 수 있습니다.<br>
즉 새로운 요소를 움직이거나 추가,삭제를 할 수 있게 해줍니다.

<br>
예를 들자면 아래와 같이 html 요소중에 class가 .box1 태그의 글 색상을 빨간색으로 변경

```js
document.querySelector('.box1').style.color = 'red';
```

### 3.2 BOM(Browser Object Model)

BOM은 브라우저에 관련된 객체들의 집합입니다.<br>
**문서 객체 모델(DOM, Document Object Model)**이라고 통합해서 부르기도 합니다.

- #### location 객체
  현재 표시된 브라우저의 HTML 문서의 주소(URL)값을 얻거나, 새 문서를 불러올 때 사용할 수 있습니다.<br>
- #### navigator 객체
  브라우저의 버전과 같은 다양한 정보를 저장하는 객체입니다.
- #### screen 객체
  브라우저 화면이 아닌 사용자의 디스플레이와 사용 가능한 색상수에 관련된 다양한 정보들을 저장하는 객체입니다.
- #### history 객체
  브라우저의 히스토리 정보를 문서와 상태 목록으로 저장하는 객체입니다. <br>
  <span style="color:red">javascript는 개인 정보를 보호하기 위해 일부 제한적으로 객체 접근을 허용합니다.</span>

### 3.3 JavaScript

DOM에서 설명한 것과 같이 DOM은 자바스크립트와 같은 스크립팅 언어를 사용해서 DOM을 제어할 수 있다고 했습니다. <br>
이러한게 가능한 이유는 결국 Window 객체에 **DOM,BOM**이 포함되어 있기 때문에 자바스크립트를 통해 **DOM에 관련된 API**, **BOM에 관련된 API**를 사용할 수 있는 것입니다.

> [데브쿠마](http://www.devkuma.com/books/pages/192)
