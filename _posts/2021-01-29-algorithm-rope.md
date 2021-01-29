---
title: '그리디 알고리즘 로프'
excerpt: 'javascript를 사용해서 백준알고리즘 그리디 로프 문제를 풀겠습니다.' 
categories: [algorithm]
tags: [알고리즘 로프, 자바스크립트 알고리즘, 그리디 알고리즘]
last_modified_at: 2021-01-29T01:20:00-21:00 
toc: true 
toc_label: '목차'
---

## 문제

N(1 ≤ N ≤ 100,000)개의 로프가 있다. 이 로프를 이용하여 이런 저런 물체를 들어올릴 수 있다. 각각의 로프는 그 굵기나 길이가 다르기 때문에 들 수 있는 물체의 중량이 서로 다를 수도 있다.

하지만 여러 개의 로프를 병렬로 연결하면 각각의 로프에 걸리는 중량을 나눌 수 있다. k개의 로프를 사용하여 중량이 w인 물체를 들어올릴 때, 각각의 로프에는 모두 고르게 w/k 만큼의 중량이 걸리게 된다.

각 로프들에 대한 정보가 주어졌을 때, 이 로프들을 이용하여 들어올릴 수 있는 물체의 최대 중량을 구해내는 프로그램을 작성하시오. 모든 로프를 사용해야 할 필요는 없으며, 임의로 몇 개의 로프를 골라서 사용해도
된다.

### 입력

첫째 줄에 정수 N이 주어진다. 다음 N개의 줄에는 각 로프가 버틸 수 있는 최대 중량이 주어진다. 이 값은 10,000을 넘지 않는 자연수이다.

### 출력

첫째 줄에 답을 출력한다.

### 예제 입력 1

```
2
10
15
```

### 예제 출력 1

```
20
```

## 풀이

- **문제의 핵심**
	- 최대중량을 구하는데 단 하나의 로프라도 끊어지면 안됨.
	- 단 모든 로프를 사용해야 할 필요가 없음.
	- 임의로 몇 개의 로프를 골라서 사용해도 된다.
	- 병렬로 연결하여 k개의 로프를 사용해서 중량이 w인 물체를 들어올릴 때, 각각의 로프에는 w/k만큼의 중량이 걸리게 된다.
	
	
- **코딩 접근 방식**
  - 리스트를 내림차순으로 정렬한다.
  - 간단하게 최대로 버틸 수 있는 로프 중량을 먼저 구한다. (로프 1개)
  - 예를 들어 0번째 로프 중량이 20이라면 1번째 로프 중량은 내림차순 정렬 했기 때문에
	`list[0] >= list[1] >= list[n]..` 이다. <br> list[1] * 2(로프2개)를 해도 무게는 w/k만큼 분산 되기 때문에 결국은
	  list[0] >= (list[1] * 2)/2 이기 때문에 로프가 끊어질 일은 없다. (로프 2개)
	

### 코딩

```js
const readline = require('readline');
const rl = readline.createInterface({
	input : process.stdin,
	output: process.stdout
})

// 로프 k
let k = 0;
// 각로프 최대버틸 수 있는 무게 리스트
let weightList = [];
// 최대 중량
let max = 0;

// 입력 조건 변수
let count = 0;

rl.on('line', ( line ) => {
	if (count === 0) {
		k = parseInt(line.trim())
	} else {
		weightList.push(parseInt(line.trim()))
	}
	if (count === k) {
		rl.close();
		getMaxWeight(k, weightList);
	}
	count++;
})

function getMaxWeight( k, weightList ) {
	weightList.sort(( a, b ) => b - a); // 내림차순 정렬
	for (let i = 1; i <= k; i++) {  // i 는 사용한 로프 갯수
		if(weightList[i-1] > max) {
			max = weightList[i-1] * i;
		}
	}
	console.log(max);
}

```

---

**참고** <br>
[백준 그리디 알고리즘 2217번](https://www.acmicpc.net/problem/2217){:target="\_blank"} <br>