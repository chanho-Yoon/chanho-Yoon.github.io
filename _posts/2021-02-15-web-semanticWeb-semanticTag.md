---
title: 'Semantic Web, Semantic Tag 이해'
excerpt: 'semantic web, semantic tag에 대해 알아보도록 하겠습니다.' 
categories: [web]
tags: [semantic web, semantic tag, wecode]
last_modified_at: 2021-02-15T01:18:00-19:00, 
toc: true 
toc_label: '목차'
sitemap :
changefreq : daily
priority : 1.0
---

> semantic web과 semantic tag에 대해 어렴풋이 알고 있었지만, 이번 위코드 1일차에 주어진 과제에서 "사이트에 이미지를 넣는 방법은 `<img>` 태그를
> 사용하는 방법과 태그 속성에 `background-image` 속성을 추가하는 것이 있다. 두 가지 방법의 차이점과 각각 어떠한 경우에 사용하면 좋은지 설명하시오"
> 라는 질문에 답을 하기 어렵다는 사실을 알았다.... 면접에도 자주 등장하는 질문이니 이번 기회에 확실히 알아보도록 하겠습니다.

## 1. Semantic web

### 1.1 Semantic web이란?

**Semantic Web**은 '의미론적인 웹'이라는 뜻으로, **기계가 이해할 수 있는 형태로 제작된 웹을 의미**합니다. <br>
또 사람의 머리 속의 언어에 대한 이해를 컴퓨터 언어로 표현하고 이것을 컴퓨터가 사용할 수 있게 만다는 것을 말합니다. <br>
결론적으로 **Semantic Web**은 웹에 존재하는 수많은 웹들의 메타데이터를 부여하여, 잡다한 데이터 집합이 아닌 **'의미'** 와 **'관련성'**을
가지는 거대한 데이터베이스를 구축하고자 하는 발상입니다.

> semantic web을 고안해서 semantic tag들이 나오게 되었습니다.

간단한 예시로 과거 시맨틱 웹이 고안되기 전 

```html
<div id="header"></div>
```

고안 후

```html
<header></header>
```

고안 후 컴퓨터는 이 부분이 header라는 것을 이해할 수 있게됩니다.

## 2. Semantic tag

### 2.1 Semantic tag란?

**시맨틱 웹**에서 사람과 기계가 이해할 수 있는 형태, 즉 활용하기 좋은 형태의 데이터로 웹을 발전시키기 위해 나온 **tag** 입니다. <br>
조금 더 쉽게 말하자면 HTML5 언어에 익숙하지 않는 사람이 보고도 저 태그가 무엇을 의미하는지 알아볼 수 있도록 하는 태그를 **Semantic Tag**라고 합니다.

### 2.2 Semantic Tag들

<img src='/assets/images/semanticTag.png' alt='profile' style="width:60%; margin-top:15px; margin-bottom:15px; box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px, rgba(0, 0, 0, 0.024) 0px -6px 16px -6px;"/>

| tag | <center>설명</center>                                         |
| :------: | :------------------------------------------------------------ |
|  `<header>`   | 페이지 상단이나 섹션의 머리말                                   |
|  `<nav>`  | 문서의 네비게이션, 메뉴 항목을 정의 |
|  `<section>`   | 문서의 구획들을 정의                               |
|  `<article>`  | 본문 |
|  `<aside>`  | 글의 주제와 간접적으로만 연관된 부분을 나타냄 |
|  `<details>`  | 추가적인 정보를 사용자가 숨기거나 보일 수 있게함 |
|  `<summary>`  | 부모요소인 details 요소의 내용에 대한 요약이나 캡션등을 나타냄 |
|  `<figure>`  | 사진, 다이어그램 등과 같은 부가적인 요소를 정의 |
|  `<main>`  | 문서의 주가 되는 컨텐츠 정의 |
|  `<mark>`  | 하이라이트 또는 참조와 같은 표시를 필요로 하는 문자를 정의 |
|  `<time>`  | 날짜, 시간을 정의 |
|  `<img>`  | 이미지 |
|  `<video>`  | 비디오(영상) |
|  `<audio>`  | 사운드(소리) |

등이 있다.

## 3. 결론

### 3.1 그래서 img 태그와 backgorund-img 속성 차이점이 무엇일까?

**img tag**는 결국 의미가 있는 **시맨틱 태그**로써 컴퓨터가 이해할 수 있고 `alt` 속성으로 에러 발생시 이미지가 깨져도 어떠한 이미지인지 알 수 있지만
**background-image**는 의미있는 태그가 아닌 그냥 속성으로 에러시 어떠한 이미지인지 어떠한 정보도 알 수 없습니다. 또 컴퓨터는 이 태그가 어떤 이미지인지 알 수 없습니다.

<br>

결론은 사용자를 위한 에러시 이미지가 깨져도 어떠한 이미지인지 정보가 들어가야하고 조금 더 검색엔진에 의해 웹이 잘 노출 되도록 하기 위해선 **시맨틱 태그**인 **img tag**를 사용하고,
그저 웹 디자인과 같은 미적요소로 이미지를 보여주기 위해서는 **background-image**를 사용하는게 좋을 것 같습니다.

---

**참고** <br>
[wikipedia](https://ko.wikipedia.org/wiki/%EC%8B%9C%EB%A7%A8%ED%8B%B1_%EC%9B%B9){:target="\_blank"} <br>


