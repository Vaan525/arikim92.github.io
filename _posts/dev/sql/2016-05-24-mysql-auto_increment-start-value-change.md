---
layout: post
comments: true
date: 2016-05-24
title: "auto_increment 시작 값 변경하기 ( 인덱스 재설정 )"
description: "자동으로 지정된 idx 값을 원하는 값으로 변경"
subject: dev
categories: [ sql ]
tags: [ sql, mysql, auto_increment ]
---

테스트 후 인덱스를 되돌리고 싶을 때 ~ 'ㅅ'/
3번까지 글이 있고, 4번부터 다시 시작하고 싶을 때!

```sql
alter table [테이블명] auto_increment = 4;
```
