---
layout: post
comments: true
date: 2017-04-26 15:36:00
title: "깃허브페이지에서 목차 사용하기"
description: "홈페이지에 목차 자동생성하기"
subject: blog
categories: [ tip ]
tags: [ tip, js, list-of-tables ]
---

새 포스트를 추가하면서 목차 기능을 넣었습니다.

미리보기: [미리보기](/2017/tip/facebook-login-connect){: target="_blank"}

나중에는 디자인도 바꿀 예정이지만 간단하게 넣어봤습니다 :)

> 지금은 레벨업 했다고 좋아하지만 나중에 보면 이런걸 가지고 좋아했단말이야 !?!?!? <br>
> 라고 할 수 도 있겠네요 ... :( 레벨업레벨업 !!

아래의 html 을 미리 넣어놓으면 ,

포스팅에 `h2` 태그로 된 제목들이 존재하는지 확인 후에

`ol` 태그와 `li` 태그를 넣어서 목차를 만들게 됩니다.

`ol` 태그를 사용한 이유는 숫자 목차를 만들려고 했었는데요 ,

저의 깃허브 포스팅은 `section.post-wrap` 으로 되어있습니다. (참고!)

지금 반응형으로 구성되어있는데도 무너지지 않아서 좋더라구요 ..!

> html

```html
<div class="list-of-tables"><p>목차</p></div>
```

> css ( 포스팅의 오른쪽으로 정렬 )

```css
.post-wrap .list-of-tables {
    position: relative;
    width: 14em;
    float: right;
    padding: 0.5em;
    font-size: 0.8em;
    background: #f3f3f3;
    border: 1px solid #f3f3f3;
    border-radius: 6px;
    margin-left: 1em;
}

.post-wrap .list-of-tables > p {
    margin: 0;
    position: absolute;
}

.post-wrap .list-of-tables > ol {
    margin-top: 1.8em;
    padding-left: 0.5em;
    list-style: none;
}
```

> javascript

```javascript
// 로딩 시 체크
$(window).load(function() {
    // 목차 태그가 있다면 제목을 찾는다.
    if ( $('.post-wrap').find('.list-of-tables') ) {
        var subject = $('.post-wrap').find('h2');

        // ol tag 추가
        $('.list-of-tables').append('<ol>');
        // li tag 추가
        for ( var i = 0; i<subject.length; i++ ) {
            $('.list-of-tables ol').append(
                '<li><a href="#' + subject[i].id + '">' + subject[i].textContent + '</a></li>'
            );
        }
    }

});
```
