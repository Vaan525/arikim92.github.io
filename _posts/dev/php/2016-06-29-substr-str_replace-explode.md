---
layout: post
comments: true
date: 2016-06-29
title: "단어 가지고 놀기 - substr, str_replace, explode"
description: "문자열 자르기, 바꾸기, 나누기"
subject: dev
categories: [ php ]
tags: [ php, substr, str_replace, explode ]
---

## 1. substr( string, start, length )<a id="1-substr-string-start-length-" href="#1-substr-string-start-length-" class="s-link" aria-hidden="true"></a>

> 문자열의 일부를 반환합니다.
> <http://www.w3schools.com/php/func_string_substr.asp>{: target="_blank"}

```php
<?php
substr( "Hello world", 7 );
> orld

substr( "Hello world", 0, 3 );
> Hel
?>
```

## 2. str_replace( find, replace, string, count )<a id="2-str_replace-find-replace-string-count-" href="#2-str_replace-find-replace-string-count-" class="s-link" aria-hidden="true"></a>

> 문자열에서 다른 문자로 일부 문자를 대체합니다.
> 대소문자를 구별합니다.
> <http://www.w3schools.com/php/func_string_str_replace.asp>{: target="_blank"}

```php
<?php
str_replace( "찾을문자열", "치환할문자열", "대상문자열" );

$test = str_replace("-", "", "a-b-c-d-e");
> abcde
?>
```

## 3. explode(separator, string, limit)<a id="3-explodeseparator-string-limit" href="#3-explodeseparator-string-limit" class="s-link" aria-hidden="true"></a>

> 배열로 문자열을 나누기.
> 분리 할 매개변수가 빈 칸일 수 없습니다.
> <http://www.w3schools.com/php/func_string_str_explode.asp>{: target="_blank"}

```php
<?php
$arr = explode( "+++", "A+++B+++C" );

> $arr[0] = "A"
> $arr[1] = "B"
> $arr[2] = "C"
?>
```
