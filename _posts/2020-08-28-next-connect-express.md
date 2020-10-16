---
title: 'next, express 연결'
excerpt: 'next와 express를 연결하는 이유와 방법에 대해 공부해보도록 하겠습니다.'
categories: [next, express]
tags: [next, express, next express 연결]
last_modified_at: 2020-08-28T01:17:00-18:00
toc: true
toc_label: '목차'
---

<br>

> React 클론 코딩 인강을 듣는 중에 트위터와 비슷하게 클론코딩하면서 <br>`프론트`와 `백엔드` 서버를 나눠서 개발하는데 알아뒀으면 하는 정보를 정리해보려고 합니다.

## next + express 연결하는 이유

트위터를 클론 코딩하면서 구현하는 기능중에 **팔로워**, **팔로우**, **좋아요** 등 클릭시 해당하는 유저의 데이터(id)를 받아와야 하는데 next.js는 `:/id` or `/like/:id`와 같은 동적 주소을 처리하지 못합니다.<br>
이러한 문제를 해결할 수 있는 방법은 `express`를 사용하면 해결 가능한 문제입니다.<br>
`프론트`에 `express`를 연결하면 된다.

## next + express 연결

먼저 아래와 같이 입력해서 express 서버를 만드는데 필요한 package를 install 해야합니다.<br>

```shell
$npm i express-session cookie-parser morgan dotenv
$npm i -D nodemon
```

back폴더에서 서버인 index.js에서 아래와 같은 코드를 추가해줘야 합니다.

```js
app.use(
  cors({
    origin: true,
    credentials: true,
  }),
);
```

이와 같이 추가해준 이유는 프론트 서버와 백엔드 서버의 포트번호가 다른 것을 해결해주는 미들웨어로 위와 같이 cors를 사용해서 origin, credentials true로 해주면 서로 쿠키를 주고 받을 수 있게 됩니다.

### 프로젝트 구조

```
.
├── back
│   ├── config
│   ├── migrations
│   ├── models
│   ├── node_modules
│   ├── passport
│   ├── routes
│   └── seeders
└── front
    ├── components
    ├── node_modules
    ├── pages
    ├── reducers
    ├── sagas
    └── styles
```

front 폴더에도 `express 서버`를 생성하기 위해 `server.js` 파일을 만들어줍니다.

### server.js 생성

```js
// next 와 express 연결

const express = require('express');
const expressSession = require('express-session');
const next = require('next');
const morgan = require('morgan');
const cookieParser = require('cookie-parser');
const dotenv = require('dotenv');

const dev = process.env.NODE_ENV !== 'production';

const app = next({ dev });
const handle = app.getRequestHandler(); // app에서 뽑아온 get요청 처리기

dotenv.config();
app.prepare().then(() => {
  const server = express();
  server.use(morgan('dev'));
  server.use(express.json());
  server.use(express.urlencoded({ extended: true }));
  server.use(cookieParser(process.env.COOKIE_SECRET));
  server.use(
    expressSession({
      resave: false,
      saveUninitialized: false,
      secret: '',
      cookie: {
        httpOnly: true,
        secure: false,
      },
    }),
  );
  server.get('/hashtag/:tag', (req, res) => {
    return app.render(req, res, '/hashtag', { tag: req.params.tag });
  });
  server.get('/user/:id', (req, res) => {
    return app.render(req, res, '/user', { tag: req.params.id });
  });
  server.get('*', (req, res) => handle(req, res));

  server.listen(3060, () => {
    console.log('next + express running on : http://localhost:3060');
  });
});
```

백엔드에서 express 연동할 땐 `const app = express()`지만 프론트에서 next와 express를 연결할 땐 `const app = next({dev})`와 같이 사용합니다.

<br>

```js
app.prepare().then(() => {
  ...
});
```

위와 같은 부분이 next에 필요한 부분입니다. <br>
저안에 express 코드를 적어 사용하면 둘이 연결 되는 것입니다.

<br>

```js
server.get('/hashtag/:tag', (req, res) => {
  return app.render(req, res, '/hashtag', { tag: req.params.tag });
});
server.get('/user/:id', (req, res) => {
  return app.render(req, res, '/user', { tag: req.params.id });
});
server.get('*', (req, res) => handle(req, res));
```

- `return app.render(req, res, '/hashtag', { tag: req.params.tag });` 이 부분은 app이 next이기 때문에 next를 사용해서 요청응답을 넣어주는 것입니다. <br>
- `, '/hashtag');` 이것의 의미는 해쉬태그를 클릭했을 시 실제로 보여지는 해쉬태그 페이지를 보여주는 것입니다.<br>
- `, { tag: req.params.tag }` 이건 이제 해당 페이지로 넘어갈 때 `tag`라는 정보도 같이 보내줍니다.

### package.json 수정

```json
"scripts": {
    ...
    "dev": "nodemon",
  },
```

이제 next로 프론트 서버를 구동하는게 아닌 백엔드와 같이 nodemon으로 서버를 구동한다.<br>
`nodemon`을 사용할 경우 `nodemon.json`이 필요! 아래와 같이 생성

### nodemon.json 생성

```json
{
  "watch": ["server.js", "nodemon.json"],
  "exec": "node server.js",
  "ext": "js json jsx"
}
```

next가 아닌 nodemon을 통해서 node server.js 라면 `express`가 구동되면서 `next`도 같이 구동되도록 하는 개념입니다.

## next + express 연결 의문점

- next 서버와 express 서버가 따로 구동되는게 아니라 서로 이어진다고 합니다.
