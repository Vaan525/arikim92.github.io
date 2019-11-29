---
layout: post
comments: true
date: 2017-04-10
title: "php 한글 문자열 자르기"
description: "mb_strlen, mb_substr 사용하기"
subject: dev
categories: [ php ]
tags: [ php, strlen, substr ]
---

한글 문자열을 자를 때 그냥 `substr` 함수를 자르면 글자가 깨지는걸 보신 적이 있을거에요 !

`mb_substr` 로 한글을 안전하게 자릅시다 ..!

## 1. mb_strlen<a id="1-mb_strlen" href="#1-mb_strlen" class="s-link" aria-hidden="true"></a>

```php
$string = '동해물과 백두산이 마르고 닳도록';

echo strlen($string);
// result 45

echo mb_strlen($string, 'UTF-8');
// result 17
```

글자수는 14글자 이고 공백이 3칸 이네요.

`mb_strlen` 을 쓰면 한글을 1글자로 표현해 줍니다.

영어는 1byte, 한글은 3byte 이기때문에 `substr` 로 사용할 경우 45가 출력됩니다.

보통 한글은 2byte 라고 알고있지만 euc-kr 에선 2byte, utf-8 에선 3byte 라고 하네요.

저도 이번에 검색하면서 처음 알았네요 ㅎㅎ

## 2. mb_substr<a id="2-mb_substr" href="#2-mb_substr" class="s-link" aria-hidden="true"></a>

```php
$string = '동해물과 백두산이 마르고 닳도록';

echo substr($string, 0, 8);
// 동해�

echo mb_substr($string, 0, 8, 'utf-8');
// 동해물과 백두산
```

`substr` 도 위의 설명과 내용이 같습니다.

3byte 기 때문에 애매하게 8글자로 자르면 글자가 잘려서 이상한 물음표가 따라옵니다. ( 보고싶지 않아요 ㅠㅠ ! )

`mb_substr` 은 공백포함 8글자가 예쁘게 잘립니다 :)

> 테스트 해 보시는게 온몸으로 와 닿아요 ..!

## 함께보면 좋은<a id="함께보면-좋은" href="#함께보면-좋은" class="s-link" aria-hidden="true"></a>

- [php.net substr](http://php.net/manual/kr/function.substr.php){: target="_blank"}

- [php.net strlen](http://php.net/manual/kr/function.strlen.php){: target="_blank"}

- [php.net mb_substr](http://php.net/manual/en/function.mb-substr.php){: target="_blank"}

- [php.net mb_strlen](http://php.net/manual/en/function.mb-strlen.php){: target="_blank"}
