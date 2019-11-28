---
layout: post
comments: true
date: 2016-11-23
title: "제이쿼리 select box onchange"
description: "select box 변경 시 발생하는 이벤트"
subject: dev
categories: [ publishing ]
sub: [ jQuery ]
tags: [ js, jQuery, select, onchange ]
---

> 제이쿼리는 head 에 제이쿼리를 넣어주셔야 돼요.

```html
<html>
<head>
    <script src="//cdnjs.cloudflare.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
</head>
...
```

> 제이쿼리 부분만 따로 살펴볼게요 :)

```javascript
$(function(){
    // id 가 select_box 인 아이템이 변경되었을 때
    $('#select_box').change(function(){
        // id 가 select_box 인 아이템의 선택된 옵션의 value 값을 경고창으로 띄우기
        // alert( $('#select_box option:selected').val() );
        // p 태그에 결과 값 출력하기
        $('.result').text( $('#select_box option:selected').val() );
    });
});
```

> 결과

<p data-height="265" data-theme-id="0" data-slug-hash="EWJwQK" data-default-tab="js,result" data-user="toring92" data-embed-version="2" data-pen-title="selectbox onchange" class="codepen">See the Pen <a href="https://codepen.io/toring92/pen/EWJwQK/">selectbox onchange</a> by Ari Kim (<a href="http://codepen.io/toring92">@toring92</a>) on <a href="http://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>
