---
title: '그리디 알고리즘 ATM'
excerpt: 'javascript를 사용해서 백준알고리즘 그리디 ATM 문제를 풀겠습니다.' 
categories: [algorithm]
tags: [알고리즘 ATM, 자바스크립트 알고리즘, 그리디 알고리즘]
last_modified_at: 2021-01-28T01:20:00-21:00
toc: true 
toc_label: '목차'
---

## 문제

인하은행에는 ATM이 1대밖에 없다. 지금 이 ATM앞에 N명의 사람들이 줄을 서있다. 사람은 1번부터 N번까지 번호가 매겨져 있으며, i번 사람이 돈을 인출하는데 걸리는 시간은 Pi분이다. 사람들이 줄을 서는 순서에 따라서, 돈을 인출하는데 필요한 시간의 합이 달라지게 된다. 예를 들어, 총 5명이 있고, P1 = 3, P2 = 1, P3 = 4, P4 = 3, P5 = 2 인 경우를 생각해보자. [1, 2, 3, 4, 5] 순서로 줄을 선다면, 1번 사람은 3분만에 돈을 뽑을 수 있다. 2번 사람은 1번 사람이 돈을 뽑을 때 까지 기다려야 하기 때문에, 3+1 = 4분이 걸리게 된다. 3번 사람은 1번, 2번 사람이 돈을 뽑을 때까지 기다려야 하기 때문에, 총 3+1+4 = 8분이 필요하게 된다. 4번 사람은 3+1+4+3 = 11분, 5번 사람은 3+1+4+3+2 = 13분이 걸리게 된다. 이 경우에 각 사람이 돈을 인출하는데 필요한 시간의 합은 3+4+8+11+13 = 39분이 된다. 줄을 [2, 5, 1, 4, 3] 순서로 줄을 서면, 2번 사람은 1분만에, 5번 사람은 1+2 = 3분, 1번 사람은 1+2+3 = 6분, 4번 사람은 1+2+3+3 = 9분, 3번 사람은 1+2+3+3+4 = 13분이 걸리게 된다. 각 사람이 돈을 인출하는데 필요한 시간의 합은 1+3+6+9+13 = 32분이다. 이 방법보다 더 필요한 시간의 합을 최소로 만들 수는 없다. 줄을 서 있는 사람의 수 N과 각 사람이 돈을 인출하는데 걸리는 시간 Pi가 주어졌을 때, 각 사람이 돈을 인출하는데 필요한 시간의 합의 최솟값을 구하는 프로그램을 작성하시오.

### 입력

첫째 줄에 사람의 수 N(1 ≤ N ≤ 1,000)이 주어진다. 둘째 줄에는 각 사람이 돈을 인출하는데 걸리는 시간 Pi가 주어진다. (1 ≤ Pi ≤ 1,000)

### 출력

첫째 줄에 각 사람이 돈을 인출하는데 필요한 시간의 합의 최솟값을 출력한다.

### 예제 입력 1

```
5
3 1 4 3 2
```

### 예제 출력 1

```
32
```

## 풀이

- 먼저 사람의 수를 입력하고, 둘째 줄에는 각 사람이 돈을 인출하는데 걸리는 시간을 `list`로 받습니다. 
- 각 사람이 인출하는데 걸리는 시간을 가진 `list`를 오름차순으로 정렬합니다.
- 예를 들어 3 1 4 3 2를 입력했을 경우 오름차순 정렬하면 아래와 같이 정렬이 되고, 각 사람이 돈을 인출하는데 필요한 최소 시간의 합 1+3+6+9+13=32가 나오게 하면 됩니다.
  ```
  [ 1, 2, 3, 3, 4 ]
  ``` 
  
### 코딩
```js
const readline = require('readline');

const rl = readline.createInterface({
  input : process.stdin,
  output: process.stdout
});

let personnel = 0;
let personList = [];
let accumulate = 0;

let count = 0;
// 1개의 정수값 , N개의 정수값 받기
rl.on('line', ( line ) => {
  if (count === 0) {
    personnel = Number(line.trim());
  } else if (count === 1) {
    getPersonList(line.trim());
    rl.close();
  }
  count++;
});

function getPersonList( input ) {
  personList = input.split(' ').map(num => parseInt(num));
  // 오름차순 정렬
  personList.sort(( a, b ) => {
    return a - b;
  });
  
  personList.reduce(( acc, cur, i ) => {
    accumulate += ( acc + cur );
    return acc + cur;
  }, 0);

  console.log(accumulate);
}

```



---

**참고** <br>
[백준 그리디 알고리즘 11399번](https://www.acmicpc.net/problem/11399){:target="\_blank"} <br>