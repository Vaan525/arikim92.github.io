---
layout: post
comments: true
date: 2020-01-28 18:00:20
title: "바코드 Open API 사용하기"
description: "metafloor / bwip-js"
subject: blog
categories: [ javascript ]
tags: [ javascript, node.js, 바코드, open_api ]
---

# Github URL

바코드 타입, 핀 번호를 통해 바코드를 만들어서 URL 로 보여준다.

React, Node.js, Browser JS 모두 가능.

<https://github.com/metafloor/bwip-js/wiki/Online-Barcode-API>

# 변수

## 필수

- `bcid` : 바코드 유형 / 기호의 이름입니다.
- `text` : 인코딩 할 텍스트입니다.

## 선택

- `scaleX` : The x-axis scaling factor. Must be an integer > 0. Default is 2.
- `scaleY` : The y-axis scaling factor. Must be an integer > 0. Default is `scaleX`.
- `scale` : Sets both the x-axis and y-axis scaling factors. Must be an integer > 0.
- `rotate` : Allows rotating the image to one of the four orthogonal orientations. A string value. Must be one of:
    - `'N'` : Normal (not rotated). The default.
    - `'R'` : Clockwise (right) 90 degree rotation.
    - `'L'` : Counter-clockwise (left) 90 degree rotation.
    - `'I'` : Inverted 180 degree rotation.
- `padding` : Shorthand for setting `paddingtop`, `paddingleft`, `paddingright`, and `paddingbottom`.
- `paddingwidth` : Shorthand for setting `paddingleft` and `paddingright`.
- `paddingheight` : Shorthand for setting `paddingtop` and `paddingbottom`.
- `paddingtop` : Sets the height of the padding area, in points, on the top of the barcode image. Rotates and scales with the image.
- `paddingleft` : Sets the width of the padding area, in points, on the left side of the barcode image. Rotates and scales with the image.
- `paddingright` : Sets the width of the padding area, in points, on the right side of the barcode image. Rotates and scales with the image.
- `paddingbottom` : Sets the height of the padding area, in points, on the bottom of the barcode image. Rotates and scales with the image.
- `backgroundcolor` : This is actually a BWIPP option but is better handled by the bwip-js drawing code. Takes either a hex RRGGBB or hex CCMMYYKK string value.

# 예시

## 바코드 + 바코드 텍스트 + 투명한 배경

```bash
http://bwipjs-api.metafloor.com/?bcid=code128&text=AB1234567890&scale=3&includetext
```

![바코드이미지]( {{ site.img_url }}/{{ page.categories }}/barcode-open-api01.png )

## 바코드 + 바코드 텍스트 + 흰 색 배경

```bash
http://bwipjs-api.metafloor.com/?bcid=code128&text=AB1234567890&scale=3&includetext&backgroundcolor=ffffff
```

![바코드이미지]( {{ site.img_url }}/{{ page.categories }}/barcode-open-api02.png )

## 바코드 + 바코드 텍스트 + 흰 색 배경 + 여백

```bash
http://bwipjs-api.metafloor.com/?bcid=code128&text=AB1234567890&scale=3&includetext&backgroundcolor=ffffff&paddingwidth=20&paddingheight=20
```

![바코드이미지]( {{ site.img_url }}/{{ page.categories }}/barcode-open-api03.png )

## 바코드 + 임의의 텍스트 + 투명한 배경

```bash
http://bwipjs-api.metafloor.com/?bcid=code128&text=AB1234567890&scale=3&alttext=asdf
```

![바코드이미지]( {{ site.img_url }}/{{ page.categories }}/barcode-open-api04.png )

## 바코드 + 임의의 텍스트 (특수문자) + 투명한 배경

```bash
http://bwipjs-api.metafloor.com/?bcid=code128&text=%5EFNC1011234567890&parsefnc&alttext=%2801%291234567890&scale=3
```

![바코드이미지]( {{ site.img_url }}/{{ page.categories }}/barcode-open-api05.png )
