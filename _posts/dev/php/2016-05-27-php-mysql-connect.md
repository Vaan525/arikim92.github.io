---
layout: post
comments: true
date: 2016-05-27
title: "PHP MySQL 연동"
description: "php 에서 mysql 과 연동하는 방법"
subject: dev
categories: [ php ]
tags: [ php, mysql ]
---

## mysql connect<a id="mysql connect" href="#mysql connect" class="s-link" aria-hidden="true"></a>

```php
<?php
$hostname = "127.0.0.1"; // 집에서 APM 설치로 테스트 하시는 분들은 localhost 도 가능합니다.
$username = "root";
$password = "****";
$dbname = "test";

$connect_db = mysql_connect( $hostname, $username, $password ) or die( "MySQL 연결에 실패했습니다" );
$result = mysql_select_db( $dbname,$connect );

if( $result ) {
    echo "MySQL Connect 성공 !!";
} else {
    echo "MySQL Connect 실패 !!";
}

mysql_close($connect);
?>
```

## mysqli connect<a id="mysqli connect" href="#mysqli connect" class="s-link" aria-hidden="true"></a>

```php
<?php
$mysqli = @new mysqli( $host, $user, $password, $dbname );
if (mysqli_connect_errno()) {
    echo "Fail";
    print_r( mysqli_connect_error() );
    exit;
}
$mysqli->set_charset("utf8");
?>
```

## 참고 페이지<a id="참고-페이지" href="#참고-페이지" class="s-link" aria-hidden="true"></a>

- <http://php.net/manual/kr/function.mysql-connect.php>{: target="_blank"}
