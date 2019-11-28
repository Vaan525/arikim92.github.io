---
layout: post
comments: true
date: 2017-05-31 16:00:00
title: "PHP 확장자 추출"
description: "확장자를 추출하여 파일을 알아내기"
subject: dev
categories: [ php ]
tags: [ php, extract, extension, images ]
---

확장자를 구별해서 이미지 또는 다른 종류로 분류할 수 있어요.

```php
<?php
$text = "http://url/default.png";
$ext = substr(strrchr($text,"."),1); // 확장자앞 .을 제거
$ext = strtolower($ext); // 소문자 변환
if( $ext == "jpeg" || $ext == "jpg" || $ext == "png" ) {
    echo $ext; // png 추출
}
?>
```
