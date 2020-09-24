---
title: '브라우저 렌더링 과정 및 css animation 최적화'
excerpt: '브라우저 렌더링 과정과 reflow와 repaint에 대해 알아보겠습니다.'
categories: [Web]
tags: [render]
last_modified_at: 2020-09-24T01:15:00-16:00
toc: true
toc_label: '목차'
---

  <img src='/assets/images/browserrender.png' alt='profile' style="width:600px; margin-top:15px; margin-bottom:15px; box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px, rgba(0, 0, 0, 0.024) 0px -6px 16px -6px;"/>

## 브라우저 렌더링 과정

1. HTML, CSS, JS 파일 다운로드
2. HTML -> **DOM** , CSS -> **CSSOM** 으로 변환
3. DOM 과 CSSOM을 합쳐 **RenderTree**를 구성
4. RenderTree를 이용해서 window 위에서 요소들을 배치하게 되는 작업(**Layout**)을 한다.
5. Layout에서 계산한 요소들을 어떻게 배치했냐에 따라 각각의 요소들을 레이어별로 나누는 작업(**Paint**)을 한다.
6. 레이어를 순서대로 브라우저 위에다가 표기하는 과정(**Composition**)

이 전체과정을 **Critical Rendering Path** 라고 부릅니다.

## reflow 와 repaint

### reflow

element(요소)들의 크기나 위치가 바뀌게 되면 DOM,CSSOM을 새로 만드는 과정입니다. 이러한 과정은 **RenderTree**를 재생성함으로써 부하가 큽니다. **쟁크현상의 주요원인**으로 Layout에 영향을 줍니다.

> 웹페이지는 60FPS를 유지했을때 사용자가 이동을 하거나 스크롤시 이질감 없이 부드럽게 느껴지게 되는데 만일 일정하게 60FPS를 유지하지 못했을때 사용자가 스크롤을 하거나 드래그를 하게되면 화면이 버벅버벅 거리는 것처럼 느껴지게 됩니다. 이러한 현상을 **쟁크현상**이라고 합니다. <br>일반적으로 브라우저에서 크기가 변하는 요소들이 있을때(ex: 요소의 스타일이 변경되는) 초당 60프레임이 16,6ms안에 일어나야하는데 layout 또는 paint 과정을 다시 할 경우에 **쟁크현상**이 발생할 수도 있습니다.

### repaint

눈에 보이는 element(요소)들이 변경될 경우에 DOM,CSSOM을 새로 만들고 RenderTree를 다시 생성하지만 Layout단계를 건너뛰고 paint작업부터 하게 됩니다.<br>
여기서 눈에 보이는 요소들이란 color, background-color 등이 있습니다.

### reflow와 repaint를 하게 되는 css 요소들 확인

[CSS Triggers](https://csstriggers.com/)사이트에 들어가면 어떤 속성들이 값이 변했을 때 layout 또는 paint가 다시 일어나는지 알 수 있습니다.<br>

1. Blink - 크롬, 익스 엣지(최신)
2. Gecko - 파이어폭스
3. Webkit - IOS, 사파리
4. EdgeHTML - 오래된 엣지 브라우저 <br>

**Change from default** 는 최초에 브라우저가 실행됐을 때 즉 기본설정된 css 값이 바뀔때<br>
**Subsequent updates** 는 주기적으로 업데이트될 때 발생할 수 있는 절차가 나와있습니다.<br>
최대한 layout단계와 paint단계가 아닌 composition단계만 발생할수 있도록 사용하면 최적

### composition 단계로 직접 레이어를 전달하는 방법

만약 element(요소)들의 크기나 위치가 바뀐다거나 색상이 바뀌는 요소들은 transform, opacity 속성을 통해서 Layout, paint 단계를 건너뛰고 composition 단계로 직접 레이어를 전달 할 수 있습니다. 이러한게 가능한 이유는 transform, opacity는 GPU에서 관여하기 때문입니다.

### 애니메이션을 JS, CSS로 DOM요소를 조작할 때 가장 베스트

- composition만 일어나면 가장 베스트 케이스 👍🏻
- paint는 나쁘진 않지만 썩 좋지 않은 경우 🔺
- layout을 일어나게 한다면 최악의 경우 ❌

---

**참고**

> [소소](https://post.naver.com/viewer/postView.nhn?volumeNo=8431285&memberNo=34176766)<br>[NAVER D2](https://d2.naver.com/helloworld/2061385)
