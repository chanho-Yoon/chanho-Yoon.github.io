---
title: '객체지향 자바스크립트에서 클래스와 오브젝트 차이'
excerpt: '객체지향 자바스크립트에서 클래스와 오브젝트 차이에 대해 공부하겠습니다.'
categories: [JavaScript]
tags: [Javascript class, Javascript object]
last_modified_at: 2020-09-07T01:15:00-16:00
toc: true
toc_label: '목차'
sitemap :
  changefreq : daily
  priority : 1.0
---

## 1. 클래스와 오브젝트

### 1.1 클래스란?

클래스는 무언가를 만들 수 있는 틀, **템플릿**이라고도 불립니다.

클래스에는 **fields**, **methods** 가 포함되어 있습니다.

```js
class animal {
	name;  // field
	local: // field
	eat(); // method
}
```

이와 같이 관련된 변수와 함수를 묶어 놓은 것을 **클래스**라고 합니다.

클래스를 이용하여 **상속**과 **다양성**이 발생할 수 있는데 이러한 모든 것을 가능하게 하는 것이 **객체지향**입니다.

### 1.2 오브젝트란?

클래스는 무언가를 만들 수 있는 '틀' 이라고 했습니다.

**오브젝트**는 이러한 틀(클래스)로 만들어낸 것 입니다.

클래스를 이용하여 새로운 인스턴스를 생성하면 **오브젝트**가 되는 것입니다.

### 1.3 클래스와 오브젝트 차이

우리가 흔히 볼 수 있는 붕어빵을 만드는 과정을 예로 들어보겠습니다.

붕어빵 틀(클래스) → 팥을 넣었다 → 팥 붙어빵(오브젝트)

붕어빵 틀(클래스) → 크림을 넣었다 → 크림 붕어빵(오브젝트)

## 2. 클래스의 선언

```js
class Bungeoppang {
  constructor(meterial) {
    this.meterial = meterial;
  }
}
```

붕어빵을 만드는 클래스를 만들었습니다.

클래스 생성 시에 해당하는 재료를 넣을 수 있는 생성자 또한 만들었습니다.

## 3. 오브젝트 생성

```js
const redBeanBungeoppang = new Bungeoppang('redBean'); // 팥 붙어빵
const creamBungeoppang = new Bungeoppang('cream'); // 크림 붕어빵
```

```js
redBeanBungeoppang.meterial;
('redBean');
creamBungeoppang.meterial;
('cream');
```

`new` 키워드를 사용해서 오브젝트를 만드는데 재료로 '팥', '크림'을 넣었습니다.

이와 같이 클래스(틀)을 이용하여 다양한 오브젝트를 생성할 수 있습니다.

<!-- > [참고]() -->
