---
title: '릿코드 - Maximum Number of Balls in a Box 알고리즘'
excerpt: 'javascript를 사용해서 릿코드 Maximum Number of Balls in a Box 문제를 풀겠습니다.' 
categories: [algorithm]
tags: [알고리즘, 자바스크립트 알고리즘, 릿코드 그리디 알고리즘]
last_modified_at: 2021-02-04T01:20:00-21:00 
toc: true 
toc_label: '목차'
sitemap :
changefreq : daily
priority : 1.0
---

## 문제

You are working in a ball factory where you have n balls numbered from lowLimit up to highLimit inclusive (i.e., n == highLimit - lowLimit + 1), and an infinite number of boxes numbered from 1 to infinity.

Your job at this factory is to put each ball in the box with a number equal to the sum of digits of the ball's number. For example, the ball number 321 will be put in the box number 3 + 2 + 1 = 6 and the ball number 10 will be put in the box number 1 + 0 = 1.

Given two integers lowLimit and highLimit, return the number of balls in the box with the most balls.

### 예제 입력 및 출력

```
Input: lowLimit = 1, highLimit = 10
Output: 2
Explanation:
Box Number:  1 2 3 4 5 6 7 8 9 10 11 ...
Ball Count:  2 1 1 1 1 1 1 1 1 0  0  ...
Box 1 has the most number of balls with 2 balls.
```
```
Input: lowLimit = 5, highLimit = 15
Output: 2
Explanation:
Box Number:  1 2 3 4 5 6 7 8 9 10 11 ...
Ball Count:  1 1 1 1 2 2 1 1 1 0  0  ...
Boxes 5 and 6 have the most number of balls with 2 balls in 
```
```
Input: lowLimit = 19, highLimit = 28
Output: 2
Explanation:
Box Number:  1 2 3 4 5 6 7 8 9 10 11 12 ...
Ball Count:  0 1 1 1 1 1 1 1 1 2  0  0  ...
Box 10 has the most number of balls with 2 balls.
```

## 풀이

- **문제의 핵심**
  - lowLimit에서 highLimit까지 번호가 매겨진 n개의 공
  - 1에서 무한대까지 번호가 매겨진 무한한 수의 상자
  - 각 공을 공 번호의 자릿수 합계와 같은 숫자로 상자에 넣으면 됩니다. ex) 공 번호 321이면 3+2+1 = 6(상자번호)에 넣으면 됩니다.
  - 상자에서 공이 가장 많은 공의 수를 구합니다.


- **코딩 접근 방식**
  
  <img src='/assets/images/maxNumber.png' alt='profile' style="width:700px; margin-top:15px; margin-bottom:15px; box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px, rgba(0, 0, 0, 0.024) 0px -6px 16px -6px;"/>
  
  - 배열 변수를 만듭니다. `arr` ( 1에서 무한대까지 번호가 매겨진 공을 담을 상자 )
  - 몇 번의 상자에 공을 넣을지를 위한 `sum` 변수를 만듭니다.
  - 공이 가장 많이 들어있는 수를 알기 위해 `maxValue` 변수를 만듭니다.
  - 몫이 `0`이 될때까지 
    - 10으로 n(숫자공)을 나눈 나머지 값을 `sum` 변수에 저장합니다.
    - n을 10으로 나눈 몫을 다시 n에 저장합니다.
    ```js
    sum += curValue % 10;
    n = Math.floor(n / 10);
    ```

### 코딩

```js

const countBalls = (lowLimit, highLimit) => {
  let arr = [0];
  let sum = 0;
  let maxValue = 0;
  for (let i = lowLimit; i <= highLimit; i++) {
    sum = 0;
    let curValue = i;
    while(curValue !== 0) {
      sum += curValue % 10;
      curValue = Math.floor(curValue / 10);
    }
    if(!arr[sum-1])
      arr[sum-1] = 0;
    
    arr[sum-1]++;
    
    if(maxValue < arr[sum-1])
      maxValue = arr[sum-1];
  }
  return {arr,maxValue};
}

const obj = countBalls(5,15);
let maxIndex = [];

for(let i=0; i< obj.arr.length; i++) {
  if(obj.maxValue === obj.arr[i])
    maxIndex.push(i+1);
}

console.log(`ballCount : ${obj.arr}`);
console.log(`Output : ${obj.maxValue}`);
console.log(`maxIndex : ${maxIndex}`);
```

<img src='/assets/images/maxNumberOutput.png' alt='profile' style="width:700px; margin-top:15px; margin-bottom:15px; box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px, rgba(0, 0, 0, 0.024) 0px -6px 16px -6px;"/>


---

**참고** <br>
[릿코 1742](https://leetcode.com/problems/maximum-number-of-balls-in-a-box/){:target="\_blank"} <br>