---
layout: post
comments: true
date: 2020-08-04 11:41:38
title: "Node.js global variable 체크하기"
description: "global 변수 체크"
subject: dev
categories: [ nodejs ]
tags: [ nodejs, error, undefined ]
---

`global` 은 사실 많이 쓰이지 않는다. 많이 쓰여서도 안되고!

가끔 쓰게 되는일이 있었는데, 변수를 선언만 하고 아래에서 false 체크를 했더니 에러가 났다.

있는지를 체크하는데 왜 에러가 날까 (...)

정답은 간단했다. `null` 로 선언하면 된다.

막상 이런상황이 오니까 어떻게 검색해야 할지도 의문이었고, 보통 `null` 로 선언을 하지 않아서 생각지도 못했다.
    
```javascript
ReferenceError: accessToken is not defined
    at /usr/src/app/main/index.js:82:5
    ...
```
    
테스트는 `GetToken()` 호출 하는 부분을 주석하고 테스트 했다.
    
    
```javascript
// google access token 가져오기
global.accessToken;

const GetToken = async () => {
    // 코드 중간 생략
    ...

    accessToken = auth.access_token;

    // 새로 발급
    ...
};

// access token 발급
( async() => {
    GetToken();
})();

router.post("/", async (req, res, next) => {
    // 가끔 token err
    if (!accessToken) { // 여기서 에러가 났다.
        await GetToken();
    }
});
```

해결은 첫째줄을 `null` 로 바꿔주는게 끝이었다.

```javascript
// google access token 가져오기
global.accessToken = null;
```
