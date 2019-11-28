---
layout: post
comments: true
date: 2017-07-06 11:23:00
title: "카카오톡 챗봇 ( 플러스친구 ) 글자수 제한 확인하기"
description: "카카오 챗봇으로 설정할 수 있는 글자수 제한을 확인하자"
subject: blog
categories: [ chatbot ]
tags: [ dev, kakaobot, kakao, chatbot, limit ]
---

오늘은 궁금증이 생겨 간단한 테스트를 해봤습니다 !

과연 카카오 챗봇은 글자수 제한이 몇 일까 ..?

> 카카오 관리자 화면

플러스 친구 관리자 화면입니다.

스마트 채팅 중 자동응답형을 확인해보면

버튼은 20자, 응답 메세지는 400자 까지 설정이 가능합니다.

![카카오 관리자화면]( {{ site.img_url }}/{{ page.categories }}/dev-character-limit01.png )

따로 개발은 API형에서 하고 있으니 이걸로 테스트를 해보겠습니다 !

200자 400자 800자 .. 1000자를 넘기고서 2500자에 도전을 해보았더니 !!

![카카오 챗봇화면]( {{ site.img_url }}/{{ page.categories }}/dev-character-limit02.jpg )

드디어 짤렸어요. [ 팔 ] 에서 잘렸어요.

복사해서 콘솔창에 찍어봤더니 [ 2058자 ] 라는 결과가 나왔습니다.

왜죠... 2058자라니... 왜.......

![글자수 확인화면]( {{ site.img_url }}/{{ page.categories }}/dev-character-limit03.png )

버튼은 아래 사진을 다시 보시면 50자까지 테스트 해보았지만 잘 나옵니다.

그대신 글씨 크기가 줄어드네요.

![카카오 챗봇화면]( {{ site.img_url }}/{{ page.categories }}/dev-character-limit04.jpg )

이런걸 찾아낼 수록 신기하네요 ㅋ_ㅋ
