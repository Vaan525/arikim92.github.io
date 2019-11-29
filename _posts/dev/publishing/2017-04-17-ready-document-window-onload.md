---
layout: post
comments: true
date: 2017-04-17 11:52:00
title: "document.ready, window.ready, window.onload 실행순서"
description: "document.ready, window.ready와 window.onload의 실행순서"
subject: dev
categories: [ publishing ]
sub: [ jQuery ]
tags: [js, ready, onload, document]
---

이 포스트를 쓰다보니 자바스크립트에 대해 너무 많이 모른다는 생각이 들어서

조만간 자바스크립트 포스트만 쓰게 될 것 같다. :(

스크립트의 실행 위치나, DOM 에 대한 자세한 것도 공부해서 올릴 예정 !

*****

## 1. 실행 순서<a id="1-실행-순서" href="#1-실행-순서" class="s-link" aria-hidden="true"></a>

1. document.ready
2. window.ready
3. window.onload

## 2. 설명<a id="2-설명" href="#2-설명" class="s-link" aria-hidden="true"></a>

- window.ready , document.ready
> `window.ready` 보다 `document.ready` 가 먼저 실행됩니다.<br>
> `window.ready` 는 페이지 내의 이미지를 포함하여 모든 리소스가 로드 되고나서 실행되고<br>
> `document.ready` 는 태그 등의 세팅이 완료 되었을 때 실행되기 때문입니다.

- window.onload
> `window.onload` 는 `<body onload="">` 와 같은 기능인데요 ,<br>
> 둘 다 선언된다면 `body` 의 함수가 실행되고 `window.onload` 함수는 실행되지 않습니다.<br>
> `window.onload` 함수가 두개 이상 선언되면 마지막 한 개의 함수만 실행됩니다.

## 3. 예제<a id="3-예제" href="#3-예제" class="s-link" aria-hidden="true"></a>

```javascript
$(document).ready(function(){
    console.log('document.ready');
});

$(window).ready(function(){
    console.log('window.ready');
});

window.onload = function() {
    console.log('window.onload');
};

-- RESULT
> document.ready
> window.ready
> window.onload
```

결과는 이 페이지 내에서도 확인 가능합니다. :D

<script>
window.onload = function() {
    console.log('window.onload');
};

$(document).ready(function(){
    console.log('document.ready');
});

$(window).ready(function(){
    console.log('window.ready');
});
</script>
