---
title: 'em rem 단위'
excerpt: 'em,rem 단위에 대해 알아보도록 하겠습니다.' 
categories: [css]
tags: [em rem, em, rem]
last_modified_at: 2021-01-10T01:18:00-19:00, 
toc: true 
toc_label: '목차'
sitemap :
  changefreq : daily
  priority : 1.0
---

## 1. em과 rem 단위

폰트 단위로는 사용하는 `px`과 `em`, `rem` 단위에 대해 간단히 알아보겠습니다. <br>
시작하기에 앞서 한가지 알아야할 사실은 `em`,`rem`은 폰트 값에만 적용되는게 아니라 범용적인 범위로 `padding`,
`margin`,`width` 등에도 적용됩니다.

## 2. em 단위

### 2.1 em 단위 사용

`em`은 현재 태그의 `font-size` 값을 상속 받습니다.

```html
<div class="main">
  <div class="sub">EM 단위</div>
</div>
```

```css
.main {
  font-size : 12px;
}
.sub {
  font-size : 1.2em;
}
```

`.sub` 클래스의 font-size는 12 x 1.2 = 14.4px이 됩니다. 왜냐하면 sub의 현재 태그에 `font-size`가 없기 때문에 상위 태그로부터 `font-size`를 상속받기(12px 받음)
때문입니다.<br>
조금 더 쉽게 설명하자면 <span style="color:orange">현재 태그에 `font-size`값이 없을때에만 부모태그로부터 상속을 받습니다.</span>
<br><br>
만약 아래와 같은 코드라면 `margin`은 몇`px`일까요??

```css
.main {
  font-size : 12px;
}
.sub {
  font-size : 14px;
  margin    : 2em;
}
```

정답은!! `margin`은 14px * 2로 28px 입니다! 왜냐하면 .sub 태그에 `font-size: 14px;`값이 있기 때문에 14px를 상속받았기 때문입니다. <br>
만약 .sub에 font-size가 없었다면 상위 부모태그인 `font-size: 12px` 값을 상속받아 24px이 됩니다.

### 2.2 em 단점

`em` 단위는 `rem`이 출현한 뒤로는 잘 사용하지 않습니다. 그 이유로는 예를 들어 부모에 부모에 부모에 값을 상속받을 경우 훗날에 유지보수, 수정 등을 할때 상당히 까다롭기 때문입니다. <br>
`em` 단위를 사용해야할 때는 해당 `font-size`에 따라서 `margin`이나 `padding`이 변경되어야 할 때 사용합니다.

## 3. rem 단위

### 3.1 rem 단위 사용

`rem`은 root + em으로 root는 `html`태그를 가리킵니다. 이 말은 즉 html 태그에 지정한 `font-size`가 1 rem 이 되는 것으로 
`html`태그의 `font-size`값이 10px이라면 1rem = 10px이 되는 것 입니다.<br>
`html`태그에 `font-size`가 지정되지 않은 상태에서 1rem은 default값인 16px이 됩니다. <br>

## 4. 정리

정리하자면 `em`은 현재 태그 및 부모 태그로부터 `font-size`를 상속 받았다면 `rem`은 `html` 태그의 `font-size`값이 1rem 입니다.
<br>결국 `em` vs `rem` 구도로 "뭐를 사용하는 것이 좋을까?" 보다는 상황에 알맞게 사용해서 쓰는게 가장 좋은 방법이 아닐까 생각합니다.

---

**참고** <br>
[MDN](https://developer.mozilla.org/ko/docs/Learn/CSS/Building_blocks/Values_and_units){:target="\_blank"} <br>


