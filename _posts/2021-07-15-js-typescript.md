---
title: 'TypeScript'
excerpt: 'TypeScript 정리' 
categories: [TypeScript]
tags: [typescript]
last_modified_at: 2021-07-17T01:18:00-19:00, 
toc: true 
toc_label: '목차'
sitemap :
changefreq : daily
priority : 1.0
---

# TypeScript

typescript는 브라우저가 이해하지 못하는 언어로 결국 javascript로 변환이 된 후 로드가 되어야 이해할 수 있다.
하지만 어떤 장점으로 인해 typescript를 사용하는걸까?

## TypeScript를 사용하는 이유?

기존의 자바스크립트는 `PRIMITIVE` 와 `REFERENCE` 값이 존재한다. 먼저 아래의 예제를 보겠다.

```js
typeof 1         // 'number'
typeof 'str'     // 'string'
typeof true;     // 'boolean'
typeof Symbol(); // 'symbol
```

`typeof`는 피연산자의 type의 형태를 string으로 반환하는 함수로 JS의 PRIMITIVE값으로 type을 아는데 큰 무리가 없다.
하지만 아래와 같은 `REFERENCE TYPE`은 어떨까?

```js
const productList =[{
  id: 1,
  title: 'product1',
  option: [{
    id: 124,
    name: 'option1'
  }]
}, {
  id: 1,
  title: 'product1',
  option: [{
    id: 124,
    name: 'option1'
  }]
}]
const student = {
  name: 'Jone',
  phone: 01012341234
}
const arr = ['aaa', 'bbb']

// 결과는 모두 'object'를 반환한다.
```

이와 같이 `REFERENCE TYPE`은 type을 정확하게 추론할 수 있는 방법이 없다. 정확한 type추론이 안되는 상태에서 어떠한 타입의 값이 넘어오는지 어떠한 타입의 값을 넘겨야 하는지 어떤 타입 값이 필수값인지 알 수 있는 방법이 없다. 이러한 문제점을 보완하고자 나온 것이 `typescript` 이다.

이외에도 자바스크립트와 타입스크립트의 차이점을 알아보겠습니다.

### 자바스크립트

```javascript
function numberAdd ( a,b ) {
  return a+b;
}

let number = numberAdd(1,2);
console.log(number)
number = numberAdd(1,5,8);
console.log(number)
number = numberAdd("app","le")
console.log(number)
```

두 개의 인자를 전달받아 더하는 함수이다. 함수의 이름만 보면 어떠한 함수인지 알 수 있다. <br> 
하지만 만약 인자를 잘못전달하거나, 함수의 목적과는 다른 인자를 전달했을 때 자바스크립트는 알려주지 않는다.


이것은 원래 의도했던 함수의 목적에 맞지 않는다. <br>
이러한 단점을 극복해낼 수 있는 방법이 동적타입이 아닌 정적으로 타입을 지정해주면 해결할 수 있다.

### 타입스크립트

동적타입인 자바스크립트의 단점을 보완할 수 있는 방법으로 typescript를 사용할 수 있다. <br>

```typescript
function add (a:number,b:number) {
    return a+b;
}

console.log(add(1,2))
console.log(add(1,2,3))
console.log(add("app","le"))
```


<img src='https://user-images.githubusercontent.com/54402926/126135239-5f0d1151-b209-4f41-a84e-971380d8775c.png' alt='profile' style="width:60%; margin-top:15px; margin-bottom:15px; box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px, rgba(0, 0, 0, 0.024) 0px -6px 16px -6px;"/>
<img src='https://user-images.githubusercontent.com/54402926/126135350-9afafb12-0bbe-42c0-9bf3-688cb4de702c.png' alt='profile' style="width:60%; margin-top:15px; margin-bottom:15px; box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px, rgba(0, 0, 0, 0.024) 0px -6px 16px -6px;"/>

위와 같이 함수를 직접 들여다보지 않아도 어떠한 인자 값이 전달되어야 하고, type은 뭔지 알 수 있는 장점이 있다.

또한 typescript를 사용하게 되면 개발툴을 사용함에 있어서도 자동완성 기능의 효율도 아주 좋아지는 것을 경험했다.


> TypeScript에 존재하는 기본 타입같은 경우 공식문서에 아주 정리가 잘 되어있어 그 부분을 참고하면 되겠다.

## 타입스크립트를 사용해보면서 느꼈던 장점들

먼저 작성해야할 코드가 늘어났지만, 타입을 지정하다보니 기존 자바스크립트를 이용해 함수로 인자를 전달할 때
타입이 기억나지 않는다면 해당 함수를 살펴보거나 `console.log(typeof value)` 와 같이 타입을 확인을 해야했던 경험이 있었는데
`typescript`를 사용하여 개인프로젝트를 진행할 땐 type을 일일이 확인을 할 필요가 없을뿐더러 어떠한 객체값을 넘겨받았을 때 객체에 존재하는 `property` 
들의 type또한 알 수 있어서 너무 편리했다. 그리고 개발툴 또한 `.(닷)`을 활용한 자동완성 기능 또한 매우 좋아졌다고 느꼈다.

아직은 걸음마수준이지만 타입스크립트를 꾸준히 공부하여 확장성 있게 만들어야겠다고 느꼈다.

---

**참고** <br>
[타입스크립트 공식문서](https://typescript-kr.github.io/pages/basic-types.html){:target="\_blank"} <br>


