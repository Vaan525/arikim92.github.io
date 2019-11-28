---
layout: post
comments: true
date: 2017-04-28 15:47:00
title: "우분투 nginx 에서 서브도메인 설정하기"
description: "도메인 산 김에 서브도메인을 설정해보자"
subject: dev
categories: [ linux ]
tags: [ ubuntu, nginx, subdomain ]
---

<div class="list-of-tables"><p>목차</p></div>

## 1. 환경<a id="1-환경" href="#1-환경" class="s-link" aria-hidden="true"></a>

- Server : Google Cloud Platform ( Ubuntu )

- Nginx : nginx/1.10.0 (Ubuntu)

- PHP : PHP 7.0.15-0ubuntu0.16.04.4

## 2. 도메인 설정<a id="2-도메인-설정" href="#2-도메인-설정" class="s-link" aria-hidden="true"></a>

`hosting.kr` 에서 도메인을 구매했어요.

도메인 구매한 사이트에서 `도메인 관리 - 네임서버(서브도메인) 설정 관리` 라는 메뉴를 찾아주세요.

아래 이미지를 참고해주세요.

더 자세한 설정은 미리 올라온 포스팅에서 확인해주세요 :)

이동 : [도메인 설정](/2017/tip/github-page-tistory-naver-blog-subdomain-setting)

> 참고 이미지

![도메인설정]( {{ site.img_url }}/{{ page.categories }}/20170428_160326.png )

## 3. nginx 설정<a id="3-nginx-설정" href="#3-nginx-설정" class="s-link" aria-hidden="true"></a>

nginx 설정 파일 위치를 알아야 수정하겠죠 !

> [nginx 설정파일 세팅](/2017/linux/linux-ln-command-link-s) 방법을 참고 하세요.

```bash
/etc/nginx/nginx.conf
/etc/nginx/sites-available/default
```

이렇게 두 곳이지만 오늘은 아래만 사용할게요.

사실 설정되어있는 위의 내용을 복붙하셔서

server_name 에 원하시는 서브도메인을 , root 에는 연결할 디렉토리를 ,

index 에는 사용할 우선순위를 정해주시면 됩니다.

저는 php 를 사용중이기 때문에 아래와 같이 세팅했습니다.

> /etc/nginx/sites-available/default

```bash
server {
    listen 80;
    listen [::]:80;

    server_name blog.example.com;
    root /home/blog/;
    index index.php index.html index.htm index.nginx-debian.html;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
    }
}
```

여기서 잠깐 !

세팅 했는데 index.php 가 다운로드 되나요 ?

## 4. 번외 ( php file download )<a id="4-번외-php-file-download" href="#4-번외-php-file-download" class="s-link" aria-hidden="true"></a>

저는 아래 부분을 빼먹어서 index.php 가 다운로드 되더라구요 ㅠㅠ

미래의 나는 이런실수 하지 않겠지 ? ^^

```bash
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
    }
```
