---
layout: post
comments: true
date: 2019-11-29 09:36:06
title: "마크다운에서 링크 새 창 띄우기"
description: "target blank"
subject: blog
categories: [ tip ]
tags: [ tip, markdown, target ]
---

방법은 아주 간단해요.

여태 모르고 있었는데 우연히 찾게 됐어요.

> 링크를 만드는 법

[현재 창 구글](https://www.google.com/)

```md
[링크이름](링크주소)
```

> 링크를 새 창으로 띄우는 법
> 
[새 창 구글](https://www.google.com/){: target="_blank"}

```md
[링크이름](링크주소){: target="_blank"}
```