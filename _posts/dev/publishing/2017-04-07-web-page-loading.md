---
layout: post
comments: true
date: 2017-04-07
title: "웹 페이지 로딩 시 로딩 이미지 보여주기"
description: "로딩 이미지 만들고 적용하기"
subject: dev
categories: [ publishing ]
sub: [ html, js, css ]
tags: [ js, css ]
---

## 1. 로딩 이미지 만들기<a id="1-로딩-이미지-만들기" href="#1-로딩-이미지-만들기" class="s-link" aria-hidden="true"></a>

이미지를 만들 수 있는 사이트는 꽤 있는데요 ~

색상, 크기, 종류 등을 설정할 수 있어요.

저는 <https://preloaders.net/>{: target="_blank"} 에서 무료 이미지로 만들었습니다.
```
#5e9ef2
```
![로딩]( {{ site.img_url }}/../layout/loading.gif)

## 2. 로딩 이미지 적용하기<a id="2-로딩-이미지-적용하기" href="#2-로딩-이미지-적용하기" class="s-link" aria-hidden="true"></a>

공통으로 쓰는 페이지는 이름을 `common` 으로 사용 하고 있습니다.

파일로 따로두지 않고 `<head>` 에 넣어 사용하셔도 돼요!

> common.js

```javascript
// 윈도우가 다 load 되고 나서 id="load" 인 항목을 감춰줍니다.

$(window).load(function() {
    $('#load').hide();
});
```

> index.html

```html
// div 는 전체 화면을 반투명하게 보여주는 역할을 합니다.

<div id="load">
    <img src="{{ site.img_url }}/../layout/loading.gif" alt="loading">
</div>
```

> common.css

```css
#load {
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    position: fixed;
    display: block;
    opacity: 0.8;
    background: white;
    z-index: 99;
    text-align: center;
}

#load > img {
    position: absolute;
    top: 50%;
    left: 50%;
    z-index: 100;
}
```

## 참고 블로그<a id="참고-블로그" href="#참고-블로그" class="s-link" aria-hidden="true"></a>

- [이미지 만들기 https://www.cmsfactory.net/node/11085](https://www.cmsfactory.net/node/11085){: target="_blank"}

- [이미지 보이기 http://zent.tistory.com/86](http://zent.tistory.com/86){: target="_blank"}
