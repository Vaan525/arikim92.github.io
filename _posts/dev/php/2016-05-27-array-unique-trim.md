---
layout: post
comments: true
date: 2016-05-27
title: "배열에서 중복된 값 제거 후에 순차적으로 재정렬 하는 법"
description: "php 배열 정렬"
subject: dev
categories: [ php ]
tags: [ php, array_unique, trim ]
---

긴 말 필요없이 예제로 보시죠 :)

```php
<?php
$inp = array();
$temp = array();
$op_color = array( "red", "blue", "orange", "blue", "purple", "red", "yellow" );
$inp = array_unique( $op_color );
foreach ( $inp as $var ) {
    $var = trim ( $var );
    if (strlen ( $var )) {
        $temp [] = $var;
    }
}

print_r($inp);
?>
```

> 결과

```php
<?php Array ( [0] => red [1] => blue [2] => orange [3] => purple [4] => yellow ) ?>
```
