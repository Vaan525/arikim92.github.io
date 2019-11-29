---
layout: post
comments: true
date: 2017-07-03 15:29:00
title: "node.js 로 페이스북 메신저 사용해보기 1탄 :: nginx 를 이용하여 nodejs 서버 실행하기"
description: "nginx 를 이용하여 nodejs 서버 사용하기"
subject: dev
categories: [ nodejs ]
tags: [ nodejs, nginx ]
---

저를 위한 포스팅이에요 (!)

## 1. nginx 세팅부터<a id="1-nginx-세팅부터" href="#1-nginx-세팅부터" class="s-link" aria-hidden="true"></a>

저는 제 도메인에 서브로 node 를 넣었어요.

3000번 포트로 받을꺼에요. ( 뒤에 다시 나옵니다 ! )

```
> sudo vi /etc/nginx/sites-enabled/default
```

마지막에 아래 내용을 추가해줍니다.

```
> default

server {
    listen 80;
    listen [::]:80;

    server_name node.도메인;
    location / {
        proxy_pass http://127.0.0.1:3000;
    }
}
```

서버를 재시작 해줍니다.

```
> sudo reboot
```

## 2. nodejs 파일 작성하기<a id="2-nodejs-파일-작성하기" href="#2-nodejs-파일-작성하기" class="s-link" aria-hidden="true"></a>

이름은 쉽게 one, two 로 진행할게요 ㅋ.ㅋ

### 2-1. one.js<a id="2-1-onejs" href="#2-1-onejs" class="s-link" aria-hidden="true"></a>

one.js 를 만들어서 아래 한 줄을 작성해줍니다.

```javascript
> one.js

console.log( "Hello, World!" );
```

> 결과

```
Hello, World!
```

### 2-2. two.js<a id="2-2-twojs" href="#2-2-twojs" class="s-link" aria-hidden="true"></a>

twp.js 를 만들어서 아래 내용을 작성해줍니다.

<a href="#1-nginx-세팅부터">1번</a> 에서 3000번을 세팅 한 이유는 ,

여기서 사용되기 때문이에요.

```javascript
var http = require("http");
http.createServer(function(request, response){
    response.writeHead(200, {'Content-Type': 'text/plain'});
    response.end("Hello, World!!\n");
}).listen(3000);

console.log( "Server running at http://127.0.0.1:3000" );
```

> 결과

![set]( {{ site.img_url }}/{{ page.categories }}/nginx-node-set02.png )

## 3. 다음 이야기<a id="3-다음-이야기" href="#3-다음-이야기" class="s-link" aria-hidden="true"></a>

[node.js 로 페이스북 메신저 사용해보기 2탄 :: node.js 로 페이스북 메신저 기초세팅하기]({{ site.baseurl }}/nodejs/2017/nodejs-facebook-messenger-basic-set)

## 참고 블로그<a id="참고-블로그" href="#참고-블로그" class="s-link" aria-hidden="true"></a>

- [nginx를 이용하여 nodejs와 php 어플리케이션 함께 구동하기](http://blog.jeonghwan.net/how-to-run-nodejs-and-php-by-using-nginx/){: target="_blank"}
