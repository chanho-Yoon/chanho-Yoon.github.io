---
title: '자바스크립트 비동기적 처리'
excerpt: '자바스크립트 비동기적 처리에 대해 공부하겠습니다.'
categories: [JavaScript]
tags: [Javascript asynchronous, 자바스크립트 비동기처리]
last_modified_at: 2020-09-04T01:15:00-16:00
toc: true
toc_label: '목차'
sitemap :
  changefreq : daily
  priority : 1.0
---

## 1. 동기(synchronous) vs 비동기(asynchronous)

동기와 비동기를 나누는 큰 차이점은 실행 순서입니다.

동기는 요청을 보낸 후 해당하는 응답을 받아야만 다음으로 넘어갈 수 있는 실행방식이고

반대로 비동기는 요청을 보낸 후에 응답과 관계없이 다음 동작을 실행할 수 있는 방식입니다.

간단하게  동기와 비동기방식을 생활에 적용한 예를 들어보도록 하겠습니다.

### 1.1 동기적 방식

병원 진료를 볼때에 창구에 접수를 하기 위해서 번호표를 뽑습니다. 저의 번호표는 3번으로 저의 앞에는 1번 2번 번호표를 가진 분이 존재합니다.

1번 손님 접수요청 -> 창구에서 응답 -> 접수완료 -> 2번 손님 접수요청 -> 창구에서 응답 -> 접수완료 -> 3번 손님 접수요청 ..

위의 예시와 같이 동기적 방식은 순서가 확실히 정해져있습니다.

### 1.2 비동기적 방식

식당을 가서 음식을 주문할 때에 음식이 조리중이라서 주문 접수가 안되는 식당은 없을 것 입니다. 그리고 만일 1번째 손님이 30분 걸리는 음식을 주문하고, 2번째 손님이 5분 걸리는 음식을 주문했을 때 2번째 손님의 음식이 먼저 나올 것 입니다. 이러한 것이 비동기적 방식입니다.

만일 위의 예시에서 동기적 방식이라면, 2번째 손님은 30분을 기다려 음식을 주문해야하고 5분이라는 시간이 걸려서야 밥을 먹을 수 있게됩니다.

### 1.3 비동기적 방식을 처리하는 방법들

먼저 방법들을 설명하기에 앞서 콜백함수, promise, async/await 사용하는 이유는 비동기적 방식을 처리하는 방법들을 사용하지 않는다면 콜백 함수의 과정이 끝나기 전에 다음 프로세스로 진행될 수 있기 때문입니다. 예를 들어서 동영상 파일을 불러와 웹에 띄워줄려고 하는데 여기서 비디오 파일을 불러오는 작업이 완료되지 않았는데 다음 프로세스로 넘어가 화면에 동영상 파일을 띄워줄려고 한다면,,??

비동기적 처리 방식 사용 하지 않았을 때

const video = 비디오 파일 불러오는중(...55%) -> 다음프로세스 실행 -> video 출력 -> 에러

비동기적 처리 방식 사용

const video = 비디오 파일 불러오는중(...55%) -> 비디오 파일 (100%) 가져왔음 -> 다음프로세스 실행 -> video 정상출력

## 2. 콜백함수

콜백함수는 특정 함수에 매개변수로 전달된 함수로, 함수 안에서 어떤 특정한 시점에 다시 호출되는 함수를 말합니다.

```js
const callbackFunction = (callback) => {
  console.log('callbackFunction 실행');
  callback();
};
callbackFunction(() => console.log('전달한 callback'));
```

callbackFunction을 호출하면서 인자 값으로 console.log("전달한 callback") 반환하는 함수를 전달하였습니다.

**단점**으로는 콜백 함수가 반복되어 코드의 들여쓰기의 정도가 깊어지는 현상을 말합니다.

관련링크는 아래에 남기도록 하겠습니다.

[콜백 지옥에 대해 설명 잘된 블로그](https://librewiki.net/wiki/%EC%BD%9C%EB%B0%B1_%EC%A7%80%EC%98%A5)

## 3. **Promis**

### 3.1 promis의 사용방법

```js
//Promise 정의
const promiseData = new Promise((res, rej) => {
  res('something data');
});
//Promise 수행
promiseData.then((data) => {
  console.log(data);
});
```

Promise를 정의하고 정의할때에 인자 값으로 resolve(res), reject(rej) 인자 값을 전달합니다. 그리고 안에서 res로 어떠한 값을 전달합니다. rej는 에러를 전달

Promise 수행은 promise 객체를 담은 변수에 then을 사용하여 전달받은 data를 console.log(data)로 콘솔창에 출력하는 것을 볼 수 있습니다. then은 작업수행이 완료되면 실행이 되게 된다.

```js
//Promise 정의
const promiseData = new Promise((res, rej) => {
  setTimeout(() => res('something data'), 3000);
});
//Promise 수행
promiseData.then((data) => {
  console.log(data);
});
```

위와 같이 setTimeout 함수로 3초 뒤에 res()에 어떠한 값을 할당하는 작업이 완료되면 3초 뒤에 console.log창에 data가 출력되는 것을 볼 수 있습니다.

또 아래와 같이 promise 정의 부분을 함수로 감싸고 promise 객체를 return해서 사용할 수도 있습니다.

```js
//Promise 정의
const funcPromise = () => {
  const promiseData = new Promise((res, rej) => {
    setTimeout(() => res('something data'), 3000);
  });
  return promiseData;
};
//Promise 수행
funcPromise().then((data) => {
  console.log(data);
});
```

return 값으로 promiseData 반환

### 3.2 **Promise then의 연결 / 순서대로 처리**

만일 순서대로 비동기를 처리해야 할 때는 then을 연결하여 해결할 수 있습니다. 예제는 아래와 같습니다.

```js
//Promise 정의
const funcPromise1 = () => {
  const promiseData = new Promise((res, rej) => {
    setTimeout(() => res('something data 1'), 4000);
  });
  return promiseData;
};

const funcPromise2 = () => {
  const promiseData = new Promise((res, rej) => {
    setTimeout(() => res('something data 2'), 2000);
  });
  return promiseData;
};

const funcPromise3 = () => {
  const promiseData = new Promise((res, rej) => {
    setTimeout(() => res('something data 3'), 2000);
  });
  return promiseData;
};

//Promise 중첩 수행
funcPromise1()
  .then((data) => {
    console.log(data);
    return funcPromise2();
  })
  .then((data) => {
    console.log(data);
    return funcPromise3();
  })
  .then((data) => {
    console.log(data);
  });
```

**promise 에러처리**는 rej를 반환하여 사용할 수 있습니다.

```js
//Promise 정의
const funcPromise1 = () => {
  const promiseData = new Promise((res, rej) => {
    const num = 1;
    if (num === 1) {
      setTimeout(() => res('something data 1'), 4000);
    } else {
      rej('1 error!!');
    }
  });
  return promiseData;
};
const funcPromise2 = () => {
  const promiseData = new Promise((res, rej) => {
    const num = 2;
    if (num === 1) {
      setTimeout(() => res('something data 2'), 4000);
    } else {
      rej('2 error!!');
    }
  });
  return promiseData;
};
```

위와 같이 어떠한 조건에 의해 에러를 출력해야 할 때 그 반환 값으로 reject(rej)를 반환하면 됩니다.

그리고 promise 수행 부분에 catch를 사용하면 됩니다.

```js
//Promise 수행
funcPromise1()
  .then((data) => {
    console.log(data);
    return funcPromise2();
  })
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.log(error);
  });
```

만약에 첫번째 then에서 에러가 났다면 그 이후 then은 실행되지 않고 catch문으로 넘어가게 됩니다.

## 4. **async / await **

async/await는 Promise 객체를 반환합니다. 그렇다는 말은 Promise 객체에서 사용하는 then을 사용할 수 있다는 말입니다.

```js
const funcAsync = async () => {
  return "async";
};

async funcAsync () {
  return "async";
};

```

위와 같이 화살표함수나 일반적인 함수 선언 방식을 사용할 수 있습니다.

**async**는 함수를 Promise로 return하는 함수로 만듭니다. 저희는 앞서 Promise에서 어떠한 값을 전달할 때 resolve(res)를 사용하여 값을 전달하였습니다. promise와는 다르게 async/await에서는 return 값으로 전달하게 됩니다. 예시는 아래와 같습니다.

```js
const funcAsync = async () => {
  return 'async';
};
funcAsync().then((result) => {
  console.log(result);
});
```

**await**는 뜻으로도 알 수 있듯이 말그대로 "기다리다"  입니다. 앞에서 비동기적 방식을 이해하셨다면 아래 코드의 결과가 뭔지 아실겁니다.

```js
const delaySecond = (sec) => {
  const promiseData = new Promise((res, rej) => {
    setTimeout(() => {
      res(console.log(sec + '초에 실행'));
    }, sec * 1000);
  });
  return promiseData;
};

const funcAsync = async () => {
  delaySecond(3);
  return 'async';
};

funcAsync().then((result) => {
  console.log(result);
});
```

await 키워드를 사용하지 않았을 때

<img src='/assets/images/notasync.png' alt='profile' style="width:300px; margin-top:15px; margin-bottom:15px; box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px, rgba(0, 0, 0, 0.024) 0px -6px 16px -6px;"/>

await 키워드를 사용했을 때

```
const funcAsync = async () => {
  await delaySecond(3);
  return "async";
};

```

<img src='/assets/images/useasync.png' alt='profile' style="width:300px; margin-top:15px; margin-bottom:15px; box-shadow: rgba(50, 50, 93, 0.25) 0px 13px 27px -5px, rgba(0, 0, 0, 0.3) 0px 8px 16px -8px, rgba(0, 0, 0, 0.024) 0px -6px 16px -6px;"/>

delaySecond가 수행이 완료되길 기다렸다가 완료 됐을때 다음 순서인 return "async"를 수행하게 됩니다.

## 5. **예외처리**

try catch 사용합니다.

```js
const funcAsync = async () => {
  try {
    await delaySecond(3);
    return true;
  } catch (error) {
    console.log(error);
    return false;
  }
};
```

---

아래는 정리가 잘된 블로그와 유튜브 영상의 링크를 첨부합니다.

게시글도 아래의 링크를 참조해서 공부 및 복습겸 작성했습니다.

> [참고 : https://velog.io/@yejinh](https://velog.io/@yejinh/%EB%B9%84%EB%8F%99%EA%B8%B0-%ED%8C%8C%ED%97%A4%EC%B9%98%EA%B8%B0) <br>
> [참고 : https://www.youtube.com/watch?v=VMO4yX7kkW8](https://www.youtube.com/watch?v=VMO4yX7kkW8)
