---
layout: post
comments: true
date: 2017-07-03 15:51:00
title: "node.js 로 페이스북 메신저 사용해보기 2탄 :: node.js 로 페이스북 메신저 기초세팅하기"
description: "facebook 메신저 nodejs 서버 사용하기"
subject: dev
categories: [ nodejs ]
tags: [ nodejs, nginx, facebook, messenger, chatbot ]
---

## 1. Facebook 앱 만들기<a id="1-facebook-앱-만들기" href="#1-facebook-앱-만들기" class="s-link" aria-hidden="true"></a>

<https://developers.facebook.com/>{: target="_blank"} 이동해주세요.

![이미지1]( {{ site.img_url }}/{{ page.categories }}/facebook-messenger-basic-set01.png )

오른쪽 상단에 내 앱 부분에 마우스오버를 하시면 [ 새 앱 추가 ] 라는 항목이 있어요.

![이미지2]( {{ site.img_url }}/{{ page.categories }}/facebook-messenger-basic-set02.png )

이메일과 앱 이름을 정해주세요. 앱 이름은 알아보기 쉽게 적어주세요.

앱을 다 생성하면 다음과 같은 화면이 나와요.

저희는 메신저를 할 예정이니 정 가운데에 메신저를 선택해주세요.

![이미지3]( {{ site.img_url }}/{{ page.categories }}/facebook-messenger-basic-set03.png )

## 2. Webhook 인증받기<a id="2-webhook-인증받기" href="#2-webhook-인증받기" class="s-link" aria-hidden="true"></a>

오늘 설정부분은 [ webhook ] 부분입니다.

![이미지4]( {{ site.img_url }}/{{ page.categories }}/facebook-messenger-basic-set04.png )

node 와 nginx 설정부분은 <a href="#3-이전-이야기">이전 글</a> 을 선택해주세요.

가이드는 페이스북에도 나와있어요. <https://developers.facebook.com/docs/messenger-platform/guides/quick-start/>{: target="_blank"}

하지만 어려움을 겪는 부분이 생겨서 (...)

아! 페이스북 메신저는 https 만 가능해요.

```javascript
> test.js

var https = require('https');
var express = require('express');
var app = express();

app.set( 'port', 3000 );
app.get( '/webhook', function(req, res) {
    if ( req.query[ 'hub.mode' ] === 'subscribe' && req.query[ 'hub.verify_token' ] === 'hoit' ) {
        console.log( "Validating webhook" );
        res.status(200).send( req.query[ 'hub.challenge' ] );
    } else {
        console.error( "Failed validation. Make sure the validation tokens match." );
        res.sendStatus(403);
    }  
});

app.listen( app.get('port'), function() {
    console.log('Node app is running on port', app.get('port'));
});
```

test.js 를 실행합니다.

```bash
$ node test.js
```

> 결과

![이미지5]( {{ site.img_url }}/{{ page.categories }}/facebook-messenger-basic-set05.png )

오잉???? 다시 페이스북에 가서 테스트를 해봐요!

콜백 URL 에는 https 로 url/webhook 을 적어주세요.

확인토큰은 소스에보면 제가 hoit (...) 이라고 써놨어요 ㅎㅎ

hoit 이라고 입력해주세요.

확인 및 저장 !

![이미지6]( {{ site.img_url }}/{{ page.categories }}/facebook-messenger-basic-set06.png )

> 결과

로그가 잘 남았네요.

[ Validating webhook ] , 성공인가봐요 ㅋㅋㅋㅋ 오예

![이미지7]( {{ site.img_url }}/{{ page.categories }}/facebook-messenger-basic-set07.png )

왼쪽에 webhook 메뉴도 생겼네요.

인증까진 완료! 수고하셨어요 :)

![이미지8]( {{ site.img_url }}/{{ page.categories }}/facebook-messenger-basic-set08.png )

## 3. 이전 이야기<a id="3-이전-이야기" href="#3-이전-이야기" class="s-link" aria-hidden="true"></a>

[node.js 로 페이스북 메신저 사용해보기 1탄 :: nginx 를 이용하여 nodejs 서버 실행하기]( /2017/nodejs/nodejs-nginx-setting-test )
