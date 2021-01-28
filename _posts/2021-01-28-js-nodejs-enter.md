---
title: 'node.js 콘솔 값 입력 받기'
excerpt: 'node.js에서 콘솔로 값을 입력 받는것을 알아보겠습니다. 코테용' 
categories: [JavaScript]
tags: [node.js, node.js 콘솔 입력]
last_modified_at: 2021-01-28T01:18:00-19:00
toc: true 
toc_label: '목차'
---

> python으로 알고리즘 공부하는 중 프론트엔드는 javascript로 코딩테스트를 많이 본다고해서 js로 시작하는데
> node.js에서는 C나 python처럼 편하게 입력할 수 있는 시스템이 없다는 것을 알게되었습니다. <br>
> 조금은 다른 방법으로 콘솔 입력 값을 받아오는 것을 알아보도록 하겠습니다.


## 1. console에 입력해보자!

자바스크립트(node.js)에는 c나 python 처럼 간단하게 입력할 수 있는 시스템이 없습니다...

### 1.1 readline

JS의 내장 모듈인 `readline` 모듈을 불러와서 인터페이스 객체를 생성해야합니다.

```js
const readline = require('readline');

const rl = readline.createInterface({
   input: process.stdin,
   output: process.stdout
});

```

rl 객체는 **event-driven** 방식으로 동작합니다. 간단히 설명하자면 키보드 입력,마우스 클릭 과 같은 자바스크립트 이벤트의 한 종류로 
`line` event를 사용해서 해당하는 값을 가져올 것 입니다. <br>
`line` 은 한 줄이 입력되는 이벤트 입니다. <br>
`close` event를 사용해서 언제까지 입력할 것인지를 알 수 있습니다. 만약 `close`가 없다면 계속해서 입력을 받을 것 입니다. 


## 2. 상황에 따라 달라지는 입력 받는 방법

> 처음 1.1 인터페이스 객체를 생성하고 `rl`을 사용하면 되겠구나 했는데!! 웬걸 입력받는 값에 따라 다르게 작성해야하다니..😂 

- 하나의 정수 입력 받기
- 무한 입력 받기
- 정수 두 개 입력 받기
- 한개의 정수 입력 받고, N개 정수 입력 받기

### 2.1 하나의 정수 입력 받기

```js
let data;

rl.on('line', ( line ) => {
  data = Number(line);
  rl.close();
})
```

### 2.2 무한 입력 받기

```js
let data;

rl.on('line', (line) => {
  data = Number(line);
})
```

만약 무한으로 입력되는 것에서 나가고 싶다면 **if 조건문**을 사용해서 `rl.close()` 넣어주면 됩니다.

### 2.3 정수 2개 입력 받기 (공백으로 구분) 

```js
let data = [];

rl.on('line', (line) => {
  data = line.split(' ').map((el) => { parseInt(el) })
   
   rl.close();
})

rl.on('close', () => {
  let data1 = data[0];
  let data2 = data[1];
})
```

### 2.4 한개의 정수를 입력 받고, N개의 정수 입력 받기

```js
let num = 0;
let numList = [];
let count = 0;

rl.on('line', (line) => {
  if(count === 0) { 
    num = Number(line.trim());
  }
  else if(count === 1) {
    getNumList(line.trim());
    rl.close();
  }
  count++;
})

function getNumList (input) {
  numList = input.split(' ').map((num) => {
    parseInt(num);
  })
}

```

---

**참고** <br>
[BlueHorn07](https://bluehorn07.tistory.com/49){:target="\_blank"} <br>
[0부터 1까지](https://jsdevlog.tistory.com/entry/%EB%B0%B1%EC%A4%80%EC%BD%94%EB%93%9C-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-2588%EB%B2%88-%EA%B3%B1%EC%85%88-Nodejs-%ED%92%80%EC%9D%B4?category=1089619){:target="\_blank"} <br>


