---
layout: post
comments: true
date: 2017-06-13 16:17:00
title: "php 배열에서 원하는 원소(값)만 제거하기"
description: "배열에서 원하는 원소(값)만 제거하기"
subject: dev
categories: [ php ]
tags: [ php, array, delete, key, value ]
---

```php
<?php
// 1 배열생성
// 2 'D'의 키 값 알아내기
// 3 2번에서 알아낸 키 값을 삭제
// 4 배열 확인하기

$array = array( 'A', 'B', 'C', 'D', 'E' );
$key = array_search( 'D', $array );
array_splice( $array, $key, 1 );
print_r( $array );

> Array ( [0] => A [1] => B [2] => C [3] => E )
?>
```
