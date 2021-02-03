---
layout: post
title: 'React 라이프싸이클'
excerpt: 'React Life Cycle에 대해 공부하겠습니다.'
categories: [React]
tags: [React Lifecycle, 리액트 라이프싸이클]
last_modified_at: 2020-09-03T01:15:00-16:00
toc: true
toc_label: '목차'
sitemap :
changefreq : daily
priority : 1.0
---

## 1. React Life Cycle

React를 사용하면 각 component 단위로 UI를 화면에 보이게할 수 있고, 다른 UI로 바꾸거나 현재 UI를 스크린에서 없앨 수 있다. 따라서 각각의 Component들은 **생성 =>** **업데이트 => 제거 **의 생명주기함수(life cycle method)를 가지고 있다. 간단하게 설명하자면 react component를 생성하고 없애는 방법을 가지고 있다.

React class component는 render 말고도 다양한 것들을 가지고 있다. 

component가 생성 될 때,

-   render 전에 호출되는 function이 존재
-   render 후에 호출되는 function이 존재

## 2. Component Lifecycle

일반적으로 자주 사용하는 것은 **굵게**, 나머지는 드물게 사용

### 2.1 Mounting
처음 실행(태어남), 컴포넌트 인스턴스가 작성되어 DOM에 삽입될 때 아래와 같은 순서로 호출
<br>
component가 mount될 때, constructor()을 먼저 호출하고 render()을 호출, 그 다음 componentDidMount() 호출

-   **constructor()**
-   static getDerivedStateFromProps()
-   **render()**
-   **componentDidMount()**

### 2.2 Updating
일반적으로 업데이트시 발생, 구성 요소를 다시 렌더링 할 때 아래와 같은 순서로 호출

-   static getDerivedStateFromProps()
-   shouldComponentUpdate()
-   **render()**
-   getSnapshotBeforeUpdate()
-   **componentDidUpdate()**

### 2.3 Unmounting
component가 죽는 것 , 이 메소드는 컴포넌트가 DOM에서 제거 될 때 호출됩니다.

-   **componentWillUnmount()**

> [참고: reactjs](https://reactjs.org/docs/react-component.html)
