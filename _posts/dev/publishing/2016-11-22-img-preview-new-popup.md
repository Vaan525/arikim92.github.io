---
layout: post
comments: true
date: 2016-11-22 13:14:00
title: "이미지 경로로 새 창 띄워서 미리보기"
description: "이미지 미리보기 새 창 띄우기"
subject: dev
categories: [ publishing ]
sub: [ jQuery ]
tags: [ js, jQuery, img, popup ]
---

이건 간단한 방법이구요, window open 으로도 열 수 있습니다.

지금은 새 창으로만 열리도록 해보겠습니다.

> html

```html
<div class="content">
    <img src=" {{ site.img_url }}/../layout/head-bg-s.jpg">
</div>
```

> css ( 필수가 아니에요. )

```css
.content img {
    cursor: pointer;
}
```

> jQuery

```javascript
$(function(){
    // 이미지 클릭 시 미리보기 띄우기
    $(".content img").click(function(){
        // $(".content img") 의 src
        var src = $(this).attr("src");
        // 현재 페이지의 메인 URL
        var host = $(location).attr("host");
        // 이미지의 전체 링크
        var url = "http://" + host + src;
        // 새 창 짜잔
        window.open(url);
    });
});
```

> 실행

<style>
.content img {
    cursor: pointer;
}
</style>
<div class="content">
    <img src="{{ site.img_url }}/assets/layout/head-bg-s.jpg">
</div>
<script>
$(function(){
    $(".content img").click(function(){
        var src = $(this).attr("src");
        var host = "blog.devari.kr";
        var url = "http://" + host + src;
        window.open(url);
    });
});
</script>
