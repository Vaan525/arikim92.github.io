---
layout: post
comments: true
date: 2019-06-11
title: "만화로 배우는 리눅스 시스템 관리 - 명령어&셸 스크립트 입문"
description: ""
subject: blog
categories: [ diary ]
tags: [ linux, 길벗 ]
---

회사에서 재미난 책을 주문해주셨다 ㅋ.ㅋ
나를 위한 저장용으로 남깁니다 :)

# 만화로 배우는 리눅스 시스템 관리 - 명령어&셸 스크립트 입문

프롤로그에 연수 명부가 꼬여서 민트 라는 직원이 시스템부로 잘못 배정된 이야기가 나온다 ..
마지막엔 '원숭이도 할 수 있다!' 라는 책이 나오는데 그 말이 너무 웃겼다 ㅋㅋ

> `SSH`: Secure SHell

SSH Client 에서 암호화된 통신경로 SSH Tunnel 을 통해 SSH Server 로 접속한다.
Remote SHell 을 쓰는데 암호화되지 않기 때문에 SSH 을 사용하게 되었다.

> `grep`: global regular expression print
>       : 파일 전체에서 정규 표현식과 일치하는 위치를 출력하라

```bash
grep -r "검색할 문자열" /home/dev
```

- -r: 서브 디렉토리까지
- -i: 대소문자 구분없이
- -E: 정규 표현식을 사용할 때
- /home/dev: 찾기 시작할 디렉토리 위치

검색할 문자열에는 정규 표현식을 사용해서 찾을 수 있다.
아래 정규식으로 "filename.txt" 라는 파일을 찾을 수 있다.

```bash
grep -r -i -E "(파일명|filename)" /home/dev
```

> `vi`: 편집기

```bash
vi "파일명"
```

- i: INSERT
- /: SEARCH
- n: NEXT

검색은 정규 표현식도 가능하다. n 으로 다음 검색 문자열을 볼 수 있다.

> `yank`: 양크, 끌어당기다

복사할 문자열 앞에서 `v` 를 누르고 복사할 문자열 까지 이동 후 `y` 를 누르면 클립보드에 복사 완료.
`Shift+p` 로 붙여넣기 할 수 있다.

`cmd+z` 는 되돌리기가 아니라 일시정지 기능이다.
`u` 로 되돌리기, `cmd+r` 은 되살리기 기능이다.


> `Ctrl + r`: history 검색 기능

내가 Terminal 에서 검색한 내용을 찾을 수 있다.

## 셸 스크립트

스크립트를 자동화시키기

> `#!/bin/bash`: 셔뱅(shebang)

스크립트를 실행하는 프로그램(인터프린터)을 지정하는 것, Hash-Bang 이라고도 함.
뒤에 프로그램 전체 경로를 적으면 스크립트를 실행하는 프로그램을 셸이 자동으로 변환해준다.
위의 내용은 `bash` 용 스크립트를 작성한다는 내용이다.

perl, ruby, node 등 으로도 사용 가능하다.

> `{$HOME}`: home directory

```bash
mkdir {$HOME}/result
```

위의 명령을 실행하면 **로그인 한 사용자**의 홈 디렉토리에 `result` 라는 폴더가 생성된다.
`arikim` 으로 로그인 했을때의 경로는 `/home/arikim` 이다.
( 아이맥에서는 `/Users/arikim` 으로 나온다. )
물론 소문자도 가능하다.

> `env`: 환경 변수 목록

```bash
Ari-iMac:~ arikim$ env
TERM_PROGRAM=Apple_Terminal
SHELL=/bin/bash
USER=arikim
LANG=ko_KR.UTF-8
.
.
HOME=/Users/arikim
LOGNAME=arikim
```

> `date`: 날짜 출력

```bash
Ari-iMac:~ arikim$ date
2019년 6월 13일 목요일 16시 54분 35초 KST
```

```bash
Ari-iMac:~ arikim$ date +%Y-%m-%d
2019-06-13
```

- 응용하기

```bash
// result.txt 파일을 만들고
Ari-iMac:Desktop arikim$ vi result.txt 
// result.txt 파일의 이름을 변경
Ari-iMac:Desktop$ mv result.txt result-$(date +%Y-%m-%d).txt 
// 폴더 내용 확인으로 변경 내용을 확인
Ari-iMac:Desktop arikim$ ls 
result-2019-06-13.txt
```
