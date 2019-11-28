---
layout: post
date: 2019-05-10
title: "아랍어 언어 속성 lang, 쓰기 방향 오른쪽에서 왼쪽으로 변경"
description: "아랍어 html 태그 추가하기"
subject: dev
categories: [ publishing ]
sub: [ dev ]
tags: [ dev, html, lang, ar ]
---

아랍어는 오른쪽에서 왼쪽으로 쓰이기 때문에 방향을 바꿔 주어야 합니다.

> `dir="rtl"`

오른쪽에서 왼쪽으로 바꾸는 방법

> `lang=ar`

언어 속성을 아랍어로 바꾸는 방법

2가지를 합쳐서 아래와 같이 사용합니다 :)

> 예제

```html
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<body>
    <div id="wrap">
        <h3>مرحبا :)</h3>
        <p>هذا هو بلوق آري.</p>
    </div>
</body>
</html>
```

![HTML예제]( {{ site.img_url }}/{{ page.categories }}/set-html-arabic-properties01.png )
