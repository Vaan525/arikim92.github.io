---
layout: post
comments: true
date: 2017-03-31
title: "자바스크립트 replace 사용하기"
description: "자바스크립트 replace 를 정규표현식으로 사용해서 replaceAll 처럼 사용"
subject: dev
categories: [ javascript ]
tags: [ js, javascript, replace ]
---

자바스크립트에서 `replace` 는 첫번째 해당 항목만 바꿔주고, 다음 항목들은 바꿔주지 않아요.

`replaceAll` 이 텍스트편집기 에서 자동완성돼서 나오지만 실제로는 사용하지 않는다고 해요.

## replace 사용<a id="replace-사용" href="#replace-사용" class="s-link" aria-hidden="true"></a>

```javascript
// 띄어쓰기 제거
var result;
var string = "A B C";
result = string.replace(" ", "");

console.log( result );
//=> AB C
```

## 정규식으로 replace 사용<a id="정규식으로-replace-사용" href="#정규식으로-replace-사용" class="s-link" aria-hidden="true"></a>

```javascript
// 정규식으로 변경
var result;
var string = "A B C";
result = string.replace(/ /g, "");

console.log( result );
//=> ABC
```

- g : 해당되는 모든것을 검색
- i : 대/소문자 구분 없이 검색
- m : 여러 줄 검색

## 정규식 활용하기<a id="정규식-활용하기" href="#정규식-활용하기" class="s-link" aria-hidden="true"></a>

```javascript
// 왼쪽 공백제거
result = string.replace( /\s+/g, "" );
// 오른쪽 공백제거
result = string.replace( /\s+$/g, "" );
// 행 바꿈 제거
result = string.replace( /\n/g, "" );
// 엔터키 제거
result = string.replace( /\r/g, "" );
```

## 참고 블로그<a id="참고-블로그" href="#참고-블로그" class="s-link" aria-hidden="true"></a>

- [cocy](http://cocy.tistory.com/24){: target="_blank"}
- [http://www.codejs.co.kr/자바스크립트에서-replace를-replaceall-처럼-사용하기](http://www.codejs.co.kr/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EC%97%90%EC%84%9C-replace%EB%A5%BC-replaceall-%EC%B2%98%EB%9F%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0/){: target="_blank"}
