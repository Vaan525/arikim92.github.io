---
layout: post
comments: true
date: 2017-04-13
title: "Form 에서 Label 사용하기"
description: "label 을 사용해서 checkbox 에 응용"
subject: dev
categories: [ publishing ]
sub: [ html ]
tags: [ html, form, label ]
---

## Form Label

label 은 두가지로 사용 가능합니다.

label 은 글씨를 선택했을 때에도 checkbox, radio 가 선택되는 기능입니다.

checkbox 를 사용해서 테스트 해 보겠습니다 :)

( radio 도 사용방법은 같습니다 !! )

label 에 `cursor: pointer;` 를 추가해주면 더 보기가 좋아지겠죠 ? ( 손가락 모양으로 마우스커서가 변경됨 )

> 첫번째

```html
<label>
    <input type="checkbox" name="chk01"> 체크해주세요.
</label>
```
<label>
    <input type="checkbox" name="chk01"> 체크해주세요.
</label>

> 두번째

```html
<input type="checkbox" name="chk02" id="check">
<label for="check">체크해주세요.</label>
```
<input type="checkbox" name="chk02" id="check">
<label for="check" style="cursor: pointer;">체크해주세요.</label>
