---
layout: post
comments: true
date: 2017-06-01 11:13:00
title: "PHP에서 ajax array, object 넘기고 받기"
description: "js 배열과 오브젝트 사용방법"
subject: dev
categories: [ php ]
tags: [ php, ajax, array, object, json ]
---

제이쿼리에서 ajax 를 사용하다 문제가 생겨서 블로그를 남깁...읍.....니다.

예시를 보시면 빠른이해가 되실거에요.

## 1. 배열 넘기기<a id="1-배열-넘기기" href="#1-배열-넘기기" class="s-link" aria-hidden="true"></a>

단순 배열은 그냥 넘기면 됩니다.

```javascript
> array

var dataArr = new Array();
dataArr[ 0 ] = 'A';
dataArr[ 1 ] = 'B';
dataArr[ 2 ] = 'C';

$.ajax({
    type : 'POST',
    url : '/test',
    cache : false,
    data : { dataArr: dataArr },
    success : function( data ){
        console.log( data );
    },
    error : function( jqxhr , status , error ){
        // console.log( jqxhr , status , error );
    }
});
```

```php
<?php
$dataArr = $_POST['dataArr'];
print_r( $dataArr );
> Array
(
    [0] => 'A'
    [1] => 'B'
    [2] => 'C'
)

echo dataArr[ 0 ];
> A
?>
```

## 2. 배열 넘기기 ??<a id="2-배열-넘기기" href="#2-배열-넘기기" class="s-link" aria-hidden="true"></a>

문제는 여기 있습니다 ..

1번에서 `$_POST['dataArr']` 로 배열을 받고있는데요 ,

아래 배열을 사용하면 넘어오지 않습니다.

원래 간단한 내용일 수 있는데요, js 의 부족한 지식과 PHP 가 만나니 이렇게 되었네요 ...

```javascript
> array

var dataArr = new Array();
dataArr['name'] = 'Ari';
dataArr['email'] = 'ari@email.com';
dataArr['phone'] = '010-1234-5678';

$.ajax({
    type : 'POST',
    url : '/test',
    cache : false,
    data : { dataArr: dataArr },
    success : function( data ){
        console.log( data );
    },
    error : function( jqxhr , status , error ){
        // console.log( jqxhr , status , error );
    }
});
```

```php
<?php
$dataArr = $_POST['dataArr'];
print_r( $dataArr );
?>
```

```
> error ...

<br />
<b>Notice</b>:  Undefined index: dataArr in <b>/test.php</b> on line <b>2</b><br />
```

## 3. key, value 형태의 배열<a id="3-key-value-형태의-배열" href="#3-key-value-형태의-배열" class="s-link" aria-hidden="true"></a>

> 달라진 점

1. new Object(); 로 선언
2. JSON.stringify( dataObject ); // object를 string형태로 변환
3. $dataObject->name; 형태로 출력

```javascript
> array

var dataObject = new Object();
dataObject['name'] = 'ari';
dataObject['email'] = 'ari@email.com';
dataObject['phone'] = '010-1234-5678';
dataObject = JSON.stringify( dataObject );

$.ajax({
    type : 'POST',
    url : '/test',
    cache : false,
    data : { dataObject: dataObject },
    success : function( data ){
        console.log( data );
    },
    error : function( jqxhr , status , error ){
        // console.log( jqxhr , status , error );
    }
});
```

```php
<?php
$dataObject = json_decode( $_POST['dataObject'] );
print_r( $dataObject );
> stdClass Object
(
    [name] => ari
    [email] => ari@email.com
    [phone] => 010-1234-5678
)

echo $dataObject->name;
> ari
?>
```
