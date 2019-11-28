---
layout: post
comments: true
date: 2017-06-13 17:24:00
title: "php 배열 정렬"
description: "배열 정렬"
subject: dev
categories: [ php ]
tags: [ php, array, sort ]
---

정렬방법은 다양하니 아래 php 사이트에서 확인해주세요 :)

<http://php.net/manual/kr/function.sort.php>

```php
<?php
$array = array( 1, 3, 5, 2, 4 );
sort( $array );
print_r( $array );

> Array ( [0] => 1 [1] => 2 [2] => 3 [3] => 4 [4] => 5 )
?>
```
