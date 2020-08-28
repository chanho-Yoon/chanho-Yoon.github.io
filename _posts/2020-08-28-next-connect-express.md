---
title: 'next, express 연결'
excerpt: 'next와 express를 연결하는 이유와 방법에 대해 공부해보도록 하겠습니다.'
categories: [next, express]
tags: [next, express]
last_modified_at: 2020-08-28T01:17:00-18:00
---

<br>

> React 클론 코딩 인강을 듣는 중에 트위터와 비슷하게 클론코딩하면서 `프론트`와 `백엔드` 서버를 나눠서 개발하는데 알아뒀으면 하는 정보를 정리해보려고 합니다.

## next + express 연결하는 이유

트위터를 클론 코딩하면서 구현하는 기능중에 **팔로워**, **팔로우**, **좋아요** 등 클릭시 해당하는 유저의 데이터(id)를 받아와야 하는데 next.js는 `:/id` or `/like/:id`와 같은 동적 주소을 처리하지 못합니다.<br>
이러한 문제를 해결할 수 있는 방법은 `express router`를 사용하면 해결 가능한 문제로, 처리하기 `프론트`에 `express`를 연결하면 된다.

## next + express 연결

먼저 아래와 같이 입력해서 express 서버를 만드는데 필요한 package를 install 해야합니다.<br>

    npm i express-session cookie-parser morgan dotenv
    npm i -D nodemon

##### 프로젝트 구조

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

##### server.js

```javascript
// next 와 express 연결

const express = require('express');
const expressSession = require('express-session');
const next = require('next');
const morgan = require('morgan');
const cookieParser = require('cookie-parser');
const dotenv = require('dotenv');

const dev = process.env.NODE_ENV !== 'production';
// const prod = process.env.NODE_ENV === 'production';

const app = next({ dev });
const handle = app.getRequestHandler();

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

  server.get('*', (req, res) => handle(req, res));

  server.listen(3060, () => {
    console.log('next + express running on : http://localhost:3060');
  });
});
```

## next + express 연결 의문점

- next 서버와 express 서버가 따로 구동되는게 아니라 서로 이어진다고 합니다.
