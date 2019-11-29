---
layout: post
comments: true
date: 2017-06-13 17:20:00
title: "php 배열 첫번째 원소삭제 / 첫번째 원소추가"
description: "첫번째 원소삭제 / 첫번째 원소추가"
subject: dev
categories: [ php ]
tags: [ php, array, value, shift, unshift ]
---

<http://php.net/manual/kr/function.array-shift.php>{: target="_blank"}

```php
<?php
// 첫번째 원소 삭제
$array = array( 'A', 'B', 'C', 'D', 'E' );
array_shift( $array );
print_r( $array );

> Array ( [0] => B [1] => C [2] => D [3] => E )
?>
```

<http://php.net/manual/kr/function.array-unshift.php>{: target="_blank"}

```php
<?php
// 첫번째 원소 추가
$array = array( 'C', 'D', 'E' );
array_unshift( $array, 'A', 'B' );
print_r( $array );

> Array ( [0] => A [1] => B [2] => C [3] => D [4] => E )
?>
```
