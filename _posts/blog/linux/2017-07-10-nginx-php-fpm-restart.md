---
layout: post
comments: true
date: 2017-07-10 12:07:00
title: "nginx 와 php-fpm 재시작하기"
description: "nginx 와 php-fpm 재시작하기"
subject: blog
categories: [ linux ]
tags: [ ubuntu, nginx, php-fpm ]
---

> nginx 재시작

```bash
sudo service nginx restart
```

> php-fpm 재시작

php5-fpm 인지 php7.0-fpm 인지 확인하고 재시작 해주세요 :)

```bash
sudo service php7.0-fpm restart
```
