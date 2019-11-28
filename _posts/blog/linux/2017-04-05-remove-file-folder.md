---
layout: post
comments: true
date: 2017-04-05
title: "리눅스 파일 또는 폴더 삭제"
description: "rm 을 이용해서 파일 또는 폴더를 삭제"
subject: blog
categories: [ linux ]
tags: [ linux, remove ]
---

## rm (remove)<a id="rm-remove" href="#rm-remove" class="s-link" aria-hidden="true"></a>

rm 은 remove 의 줄임말로 파일 또는 폴더를 삭제하는 명령어입니다.

`rm -rf` 하면 모든게 다 지워진다...는... 개발자 유머랄까요 ㅋㅋㅋ 하하하;ㅁ;

#### 1. `index.php` 파일삭제<a id="1-indexphp-파일삭제" href="#1-indexphp-파일삭제" class="s-link" aria-hidden="true"></a>

```bash
rm index.php
```

#### 2. `index.php` 파일삭제 - 삭제 시 따로 물어보지 않는다. (강제삭제?)<a id="2-indexphp-파일삭제---삭제-시-따로-물어보지-않는다-강제삭제" href="#2-indexphp-파일삭제---삭제-시-따로-물어보지-않는다-강제삭제" class="s-link" aria-hidden="true"></a>

```bash
rm -f index.php
```

#### 3. `test` 폴더삭제<a id="3-test-폴더삭제" href="#3-test-폴더삭제" class="s-link" aria-hidden="true"></a>

> 비어있지 않은 디렉토리는 -r 없이 삭제할 수 없습니다.

```bash
rm -r test/
```

#### 4. `test` 폴더안의 내용까지 모두삭제<a id="4-test-폴더안의-내용까지-모두삭제" href="#4-test-폴더안의-내용까지-모두삭제" class="s-link" aria-hidden="true"></a>

```bash
rm /test/*
```

## 참고 블로그<a id="참고-블로그" href="#참고-블로그" class="s-link" aria-hidden="true"></a>

<http://webdir.tistory.com/140>
