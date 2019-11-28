---
layout: post
comments: true
date: 2019-06-13
title: "비쥬얼 스튜디오 코드(vscode) 활용하기 3탄 :: 활용하기"
description: "sublime 에서 vscode 로 갈아타기"
subject: blog
categories: [ tip ]
tags: [ mac, editor, tip ]
---

## 시리즈

- [비쥬얼 스튜디오 코드(vscode) 활용하기 1탄 :: 설치, 세팅](/2019/tip/how-to-use-vscode-1)
- [비쥬얼 스튜디오 코드(vscode) 활용하기 2탄 :: 확장 프로그램](/2019/tip/how-to-use-vscode-2)
- [비쥬얼 스튜디오 코드(vscode) 활용하기 3탄 :: 활용하기](/2019/tip/how-to-use-vscode-3)

## vscode 활용하기

> cmd + shift + p

모든 명령을 내릴 수 있는 command 창

> 다중커서: cmd + d (연속)

같은 단어를 연속으로 계속 선택할 수 있음

> 다중커서: opt + 왼쪽 마우스 클릭

여러 포인트 동시 선택

> 다중커서: cmd + opt + 위/아래

위/아래 로 여러 포인트 동시 선택

> cmd + b

MD 파일: **글씨를 두껍게**

보통 파일: 사이드바 열기/닫기

> cmd + \

화면 분할 늘리기

누를 수록 2개, 3개, 4개...

> cmd + 숫자(n)

분할 되어있을 때 커서를 n번째로 옮김

> cmd + j

아래 터미널 창을 열기/닫기

> ctrl + j

모든 줄의 엔터를 지움

> ctrl + g

라인 이동

> cmd + u

마지막 커서 위치로 이동

> opt + 방향키(위/아래)

해당 라인 위/아래로 이동

> (cmd + k) + (cmd + x)

맨 뒤 빈 칸 삭제 ( trim )

> (cmd + k) + (cmd + f)

코드 자동정렬

> cmd + shift + v

마크다운 미리보기

> (cmd + k) + v

우측에 화면분할해서 마크다운 미리보기

( 버그인가, 타자가 쳐지지 않는다 ... )

> Emmet snippets

```html
div>ul>li
```

![Emmet-snippets]( {{ site.img_url }}/{{ page.categories }}/how-to-use-vscode05.png )

```html
<div>
    <ul>
        <li></li>
    </ul>
</div>
```
