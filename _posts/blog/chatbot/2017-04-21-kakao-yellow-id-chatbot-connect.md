---
layout: post
comments: true
date: 2017-04-21 15:39:00
title: "카카오톡 옐로아이디 서버 연동 방법"
description: "옐로아이디와 서버를 쉽게 연동하기"
subject: blog
categories: [ chatbot ]
tags: [ chatbot, kakao, yellowid ]
---

천천히 따라오시면 어렵지 않습니다!

우선 서버가 세팅되어 있어야만 진행이 가능합니다.

> 서버 세팅에 대해, 또는 이 게시글에 궁금한 점이 있으면 댓글로 남겨주세요.

[옐로아이디](https://yellowid.kakao.com/login){: target="_blank"} 홈페이지에 접속합니다.

`내 옐로아이디 관리` 를 클릭합니다.

![옐로아이디 메인]( {{ site.img_url }}/{{ page.categories }}/kakao-yellow-id01.png )

로그인 창이 나오면 로그인 해주세요.

![카카오 로그인]( {{ site.img_url }}/{{ page.categories }}/kakao-yellow-id02.png )

저희 회사 챗봇인 `튜링` 관리 페이지 입니다.

`자동응답` 탭을 클릭합니다.

![관리페이지 메인]( {{ site.img_url }}/{{ page.categories }}/kakao-yellow-id03.png )

`API형 자동응답` 에서 `설정하기` 를 클릭합니다.

![자동응답 메인]( {{ site.img_url }}/{{ page.categories }}/kakao-yellow-id04.png )

앱 이름과 앱 설명은 간단하게 작성해주세요.

앱 URL 은 `세팅되어 있는 서버 URL` 을 입력해주세요.

API TEST 를 통과하지 않으면 등록이 되지 않습니다.

![앱 수정 페이지]( {{ site.img_url }}/{{ page.categories }}/kakao-yellow-id05.png )

API TEST 를 클릭하면 아래와 같이 설정된 내용이 나옵니다.

`OK` 가 3개 다 나오지 않으면 정상적으로 작동하지 않고 등록도 되지 않습니다.

모두 입력 후 관리자 카카오톡 인증이 필요합니다.

오류가 났을 때 연락받을 관리자 카카오톡으로 인증해주세요.

모든 작업이 끝나면 저장해줍니다.

![API-TEST]( {{ site.img_url }}/{{ page.categories }}/kakao-yellow-id06.png )

다시 한번 API TEST 를 해주세요.

`서비스 시작` 버튼을 클릭해주시면 정상적으로 실행 가능합니다.

![RE-TEST]( {{ site.img_url }}/{{ page.categories }}/kakao-yellow-id07.png )

> 추가

미니홈 관리탭에서 `웰컴메세지`를 작성할 수 있습니다.

처음 플러스 친구를 등록했을 때 메세지를 보여줄 수 있습니다.

![미니홈-관리]( {{ site.img_url }}/{{ page.categories }}/kakao-yellow-id08.png )

> 적용

![적용]( {{ site.img_url }}/{{ page.categories }}/kakao-yellow-id09.jpeg)
