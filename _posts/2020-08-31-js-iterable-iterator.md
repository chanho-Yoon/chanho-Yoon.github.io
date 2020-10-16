---
title: '이터러블 프로토콜, 이터러블 / 이터레이터'
excerpt: '이터러블(iterable) 과 이터레이터(iterator)가 무엇인지 알아보도록 하겠습니다.'
categories: [JavaScript]
tags: [iterable, iterator, 자바스크립트 이터러블, 자바스크립트 이터레이터]
last_modified_at: 2020-08-31T01:17:00-18:00
toc: true
toc_label: '목차'
---

## 이터러블이란

**이터러블 프로토콜**은 ES6에서 도입된 것으로 순회(반복) 가능한 객체를 나타내는 프로토콜이다.

`for...of` 반복문, `...` 전개 연산자, 구조 분해 등과 함께 동작할 수 있도록 한 프로토콜이다.

## iterable / iterator

- 이터러블 : 이터레이터를 반환하는 `Symbol.iterator`라는 키값의 메소드를 가진 객체
- 이터레이터: `{ value, done }` 객체를 반환하는 next() 메소드를 가진 객체

## 이터러블 Symbol.iterator 객체 확인

```jsx
const arr = [1, 2, 3];

console.dir(arr);

/*
Array(3)
	> __proto__: Array(0)
		...
		> Symbol(Symbol.iterator): f values()
*/
```

위와 같이 `Symbol(Symbol.iterator): f values()` 가 존재한다는 걸 알 수 있습니다.

## 이터레이터 `{ value,done }` 반환하는 next() 객체 확인

```jsx
console.log(arr[Symbol.iterator]())

Array Iterator {}
	__proto__: Array Iterator
		> next: ƒ next()
		  Symbol(Symbol.toStringTag): "Array Iterator"
		> __proto__: Object
```

위와 같이 반환된 값이 **이터레이터**이고 next() 객체가 존재하는 것을 확인할 수 있다.

그리고 이제 {value, done} 객체를 반환하는지 console.log에 next() 메소드로 확인해보면 아래와 같이 존재하는 걸 알 수 있다.<br>

<img src='/assets/images/returniterator.png' alt='profile' style="width:300px; margin-top:15px; margin-bottom:15px; box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px, rgba(0, 0, 0, 0.024) 0px -6px 16px -6px;"/>

**value** 값이 존재할 때는 done이 **false**, 존재하지 않을때는 **true**를 가진다.
