---
title: '퀵 정렬(quick sort)'
excerpt: 'javascript를 사용해서 퀵정렬을 구현해보겠습니다.' 
categories: [algorithm]
tags: [퀵정렬, 자바스크립트 퀵정렬]
last_modified_at: 2021-02-03T01:20:00-21:00 
toc: true 
toc_label: '목차'
---

> 백준 그리디 알고리즘 2751번 수정렬하기를 풀어보면서 너무 간단하게 생각하고 반복문을 돌렸더니 "**시간초과**"로 인해 실패로 뜨는 것이었다..
> 알고보니 **퀵정렬**을 사용해서 풀어야했던 것.. 그래서 퀵정렬에 대해 정보처리기사 시험 공부할 때 기억을 되새기며 다시 복습차원에서
> 구현해보도록 하겠습니다. 
>> 머리로는 이해 되는데 코딩으로는 안짜져서 이해하는데 솔직히 이틀정도 걸린 것 같습니다.. 간단하게 sort()함수를 사용하면 될테지만 직접 구현해보는 맛도 있으니까요!!😂

## 퀵정렬

말그대로 정말 빠른 정렬입니다. 분할정복 기법을 사용합니다.<br>
**O(n log n)** 의 복잡도를 가지고 있지만 최악의 상황에서는 **O(n^2)** 복잡도를 가집니다.
<br> 여기서 최악의 상황이란 **pivot**이 계속해서 가장 작은 수 또는 큰 수가 될 경우입니다.

## 코드

> 먼저 코드를 보여드리고 설명하는게 더 좋을 것 같아서 코드먼저 올립니다!

```js
const readline = require('readline');
const rl = readline.createInterface({
	input : process.stdin,
	output: process.stdout
});

let count = 0;
let n = 0;
let arr = [];
// 입력부분 -------------------------------------------
rl.on('line', ( input ) => {
	if (count === 0)
		n = parseInt(input.trim());
	else
		arr.push(parseInt(input.trim()));
	if (count === n) {
		rl.close();
		quickSort(arr);
		console.log(arr);
	}
	count++;
});
// 입력부분 끝 -------------------------------------------
// 퀵정렬 재귀함수
function quickSort( arr, left, right ) {
	if (!left) left = 0;
	if (!right) right = arr.length - 1;
	let pivotIndex = right;

	// pivotIndex 반환
	pivotIndex = partition(arr, left, right - 1, pivotIndex);

	// pivot 보다 작은 배열 정렬
	if (left < pivotIndex - 1)
		quickSort(arr, left, pivotIndex - 1);
	// pivot 보다 큰 배열 정렬
	if (pivotIndex + 1 < right)
		quickSort(arr, pivotIndex + 1, right);

	return arr;
}

// 정렬 및 pivotIndex를 반환할 함수
function partition( arr, left, right, pivotIndex ) {
	// pivot value 값
	let pivot = arr[pivotIndex];

	// left와 right가 교차할 때 까지 반복
	while (left <= right) {
		// pivot 보다 작을경우 다음으로 넘어감
		// ( 만약 arr[left]가 pivot보다 클 경우 가만히 있고 pivot < arr[right] 로 넘어감 )
		while (arr[left] < pivot)
			left++;
		// pivot 보다 클 경우 다음으로 넘어감
		// ( 만약 arr[left]가 pivot보다 작을 경우 가만히 있고 if(left <right)로 넘어가서 swap함 )
		while (pivot < arr[right])
			right--;

		// 더이상 left와 right가 이동하지 않을 경우 서로를 swap 후 left++, right--
		if (left < right) {
			swap(arr, left, right);
			left++;
			right--;
		}
	}
	// left와 right가 교차하거나 같아진다면 left와 pivotIndex를 swap 후 left를 반환
	swap(arr, left, pivotIndex);
	return left;
}

function swap( arr, left, right ) {
	let tmp = arr[left];
	arr[left] = arr[right];
	arr[right] = tmp;
}
```

## 설명

- **pivot** 을 기준으로 pivot보다 작은 값, 큰 값으로 분할하고, 분할된 각각의 작은 값, 큰 값으로 나누어진 부분배열을 정렬합니다.
- 여기서 분할된 부분은 재귀호출을 사용합니다.
  - pivot 보다 작은 값 재귀호출
  - pivot 보다 큰 값 재귀호출
  - 재귀함수의 종료시점은 left가 right보다 커졌을 경우 return; ( 더이상 정렬할게 없다. )
- **pivot** 을 기준으로
  - left 값이 pivot보다 작으면 다음으로 넘어갑니다.
  - left 값이 pivot보다 크면 가만히 있습니다.
  - right 값이 pivot보다 크면 다음으로 넘어갑니다.
  - right 값이 pivot보다 작으면 가만히 있습니다.
  - 더이상 arr[left] < pivot && pivot < arr[right] 반복문이 동작하지 않고 `left < right` 조건문이 적합하다면 자리를 **swap** 합니다.
  - 마지막으로 left 와 right가 교차하거나 같아진다면 left와 pivotIndex를 **swap** 합니다.
  - 새로운 pivotIndex(left)를 반환합니다.
  
<img src='/assets/images/quick.png' alt='profile' style="width:700px; margin-top:15px; margin-bottom:15px; box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px, rgba(0, 0, 0, 0.024) 0px -6px 16px -6px;"/>

---

**참고** <br>
[퀵정렬 제로초](https://www.zerocho.com/category/Algorithm/post/57f72d415141fc5fe4f4ca8b){:target="\_blank"} <br>