---
layout: post
comments: true
date: 2016-09-08
title: "메모리 부족 Fatal error: Allowed memory size of ~ bytes exhausted ..."
description: "메모리 제한을 늘리는 방법"
subject: dev
categories: [ error ]
tags: [ error, php, memory ]
---

Fatal error: Allowed memory size of ~ bytes exhausted ...

에러 발생 시 제일 상단에 작성하시면 됩니다 :) ..

메모리가 부족해서 발생하는 에러인데요, 무조건 무제한으로 늘리는 건 좋지 않습니다 !!

## 1. 메모리 제한 늘리기<a id="1-메모리-제한-늘리기" href="#1-메모리-제한-늘리기" class="s-link" aria-hidden="true"></a>
```php
<?php ini_set("memory_limit", "512M"); ?>
```

## 2. 메모리 제한 무제한으로 늘리기<a id="2-메모리-제한-무제한으로-늘리기" href="#2-메모리-제한-무제한으로-늘리기" class="s-link" aria-hidden="true"></a>
```php
<?php ini_set("memory_limit", "-1"); ?>
```

## 참고 페이지<a id="참고-페이지" href="#참고-페이지" class="s-link" aria-hidden="true"></a>
<http://zetawiki.com/wiki/PHP_메모리_부족>
