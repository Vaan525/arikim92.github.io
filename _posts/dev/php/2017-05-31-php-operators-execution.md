---
layout: post
comments: true
date: 2017-05-31 15:49:00
title: "PHP 실행 연산자 (Execution Operators)"
description: "php 로 shell 명령어 사용하기 "
subject: dev
categories: [ php ]
tags: [ php, shell, execution, operators, cmd ]
---

` 를 사용하면 shell 처럼 사용할 수 있어요.

예를들어 파일을 생성할 때, 권한을 줄 수 있어요.

```php
<?php
$filepath = __DIR__."/../_log/log.json";
$file = fopen( $filepath, "w" );
`chmod 777 $filepath`;
?>
```

아주 간단해요 :) !
