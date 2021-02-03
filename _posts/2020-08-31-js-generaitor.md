---
title: '제너레이터(Generator)'
excerpt: '제너레이터(Generator)에 대해 알아보겠습니다.'
categories: [JavaScript]
tags: [Generator,제너레이터, 자바스크립트 제너레이터]
last_modified_at: 2020-08-31T01:19:00-20:00
toc: true
toc_label: '목차'
sitemap :
  changefreq : daily
  priority : 1.0
---

## 1. 제너레이터란?

ES6에서 도입된 제너레이터 함수는 **이터러블**을 생성하는 함수이다. 또한 제너레이터 함수는 비동기 처리에 유용하게 사용됩니다.

## 2. 제너레이터를 사용해야하는 이유

### 2.1 비동기 특성을 동기적 코드방식으로 관리해줍니다.

자바스크립트는 성능을 위해 비동기를 채택한다. 그 중에 가장 쉽고 흔한 방법으로는 콜백함수사용이 있다. 하지만 콜백을 중첩하게 되면 콜백지옥이라는 코드 가독성의 문제가 발생하게 된다. 이러한 문제를 해결하기 위해 프로미스가 등장 했지만 이또한 `then(), catch()`가 겹치게 되면 이것 또한 가독성이 떨어지는 문제를 일으킨다.

이러한 문제를 해결하기 위해 `async/await`가 등장 이것은 비동기적 구조를 동기적으로 작성할 수 있게 도와줍니다

제너레이터 함수도 동기적으로 작성가능한데, `async/await` 는 제너레이터 기반으로 만들어졌습니다.

### 2.2 이터레이터 이터러블을 쉽게 사용할 수 있다.

제너레이터 함수는 `next()`와 `[Symbol.iterator]()` 를 내장하고 있어 직접 `next()` 메서드와 `[Symbol.iterator]()`을 사용해야합니다.

#### 2.2.1 직접 이터레이터를 작성한 코드

- 이터레이터를 반환하는 **Symbol.iterator** 메소드를 가진 이터러블을 만들어야합니다.

```jsx
const iterableObject = {
  [Symbol.iterator]() {
    let cnt = 0;
    return {
      next() {
        cnt++;
        if (cnt < 3) {
          return { value: cnt, done: false };
        } else {
          return { value: '', done: true };
        }
      },
    };
  },
};
for (let data of iterableObject) {
  console.log(data);
}
```

- 객체가 이터러블이 되기 위해선 [Symbol.iterator]() 메서드를 가져야합니다.

#### 2.2.2 제너레이터로 다시 작성

```jsx
function* iterableObject() {
  yield 0;
  yield 1;
}
for (let data of iterableObject()) {
  console.log(data);
}
```

- 제너레이터 객체는 이터레이터 객체와 같다고 생각하면 됩니다.

> 핵심적차이는 직접 `[Symbol.iterator](), next()` 메서드를 직접 작성해서 사용하느냐 이미 구현된 `제너레이터`를 사용하느냐 차이입니다.

### 3. 코루틴 특성을 가지고 있다.

코루틴은 caller가 함수를 call하고, 함수가 caller에게 값을 return 하면서 종료하는 것에 더해 suspend, resume하여 중단된 지점부터 실행을 이어갈 수 있는 것이다.

이렇게 보면 일반함수(서브루틴)는 suspend, resume 이 빠진 코루틴이다.

> suspend(보류/정지)

> resume(되돌아감/재개)

일반적인 함수(서브루틴)는 자신의 로직을 수행한 후 콜스택에서 사라져버립니다. 또한 다시 호출했을 땐 특정 부분부터 호출할 수 있는게 아닌 무조건 함수의 "처음부터" 실행하게 되어있습니다.

이와 달리 코루틴은 종료된 함수라도 진입점을 정할 수 있게 커스터마이징 할 수 있습니다.

객체가 `yield` 표현식을 만나면 잠시 suspend되는 동시에 함수를 복사하고 콜스택을 벗어납니다. 그러다 caller가 next()메서드를 call하면 저장해 둔 스택 프레임들이 복원됩니다. suspend된 함수는 중단된 지점부터 resume 실행을 이거갑니다.

> 그래서 코루틴은 "정지→실행→정지→실행→ ..." 의 루프를 진행할 수 있습니다.

코루틴의 특성은 제너레이터(generator) 이외에도 `async/await` 도 있습니다.

### 4. 동시적인 특성을 갖고 있다.

"실행→정지→실행→정지" 코루틴의 형태를 잘 이용하면, 협력형 멀티태스킹 방식으로, 쓰레드 프로그래밍 없이 동시성 프로그래밍이 가능해진다.

### 5. 비동기적 특성을 가지고 있다.
