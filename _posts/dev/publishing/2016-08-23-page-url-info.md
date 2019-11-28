---
layout: post
comments: true
date: 2016-08-23
title: "jQuery url 정보 확인하기"
description: "현재 url 정보를 확인"
subject: dev
categories: [ publishing ]
sub: [ jQuery ]
tags: [ js, jQuery, url ]
---

## console.log 로 찍어서 확인하기

console.log 는 브라우저의 개발자 도구에서 확인할 수 있습니다.

윈도우: F12

맥: opt + cmd + i

```javascript
$(function(){
    console.log( "href: " + $(location).attr( "href" ) );
    console.log( "protocol: " + $(location).attr( "protocol" ) );
    console.log( "host: " + $(location).attr( "host" ) );
    console.log( "pathname: " + $(location).attr( "pathname" ) );
    console.log( "search: " + $(location).attr( "search" ) );
});
```

## 결과

search 는 ? 뒤의 url 내용을 보여줍니다.
post 가 아닌 get 으로 받은 변수들을 보여주게 됩니다.

![result]( {{ site.img_url }}/{{ page.categories }}/20160823_140608.png )
