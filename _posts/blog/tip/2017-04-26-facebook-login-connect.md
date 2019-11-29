---
layout: post
comments: true
date: 2017-04-26 11:45:00
title: "홈페이지에 페이스북 로그인 연동하기"
description: "페이지에 페이스북 로그인 붙이기"
subject: blog
categories: [ tip ]
tags: [ tip, facebook, login ]
---

<div class="list-of-tables"><p>목차</p></div>

홈페이지 로그인 연동에 관해 찾아보면 시간이 지난 포스트들은 이미지가 아예 다르더라구요 :(

제꺼 연동하는 김에 포스팅을 남깁니다 !!

자바스크립트로 간단하게 연동해볼게요.

<br><br>

## 1. 페이스북 로그인<a id="1-페이스북-로그인" href="#1-페이스북-로그인" class="s-link" aria-hidden="true"></a>

로그인은 하셨죠 'ㅅ'?

## 2. 페이스북 개발자센터 앱 만들고 설정하기<a id="2-페이스북-개발자센터-앱-만들고-설정하기" href="#2-페이스북-개발자센터-앱-만들고-설정하기" class="s-link" aria-hidden="true"></a>

<https://developers.facebook.com/>{: target="_blank"} 으로 들어갑니다 :)

`내 앱` 부분에 마우스를 갖다대면 `새 앱 추가` 라는 버튼이 있습니다.

![페이스북 개발자센터 메인]( {{ site.img_url }}/{{ page.categories }}/20170426_114011.png )

`표시 이름` 은 나중에도 변경 가능합니다.

`카테고리` 도 필수로 정해주시고 앱 ID 를 만들어주세요.

![새 앱ID 만들기]( {{ site.img_url }}/{{ page.categories }}/20170426_114138.png )

우선 앱을 만드셨습니다 !! 짝짝짝

이제 이 앱으로 페이스북에 관련된 모든 작업을 진행할 수 있어요.

![제품 설정]( {{ site.img_url }}/{{ page.categories }}/20170426_114214.png )

제일 상단에 Facebook 로그인이 딱 있네요 ! 시작하기를 클릭해주세요.

![빠른시작]( {{ site.img_url }}/{{ page.categories }}/20170426_115245.png )

홈페이지 주소를 페이스북에게 알려줘야 로그인 연동이 가능하겠죠 ??

왼쪽메뉴 `설정 - 기본 설정` 에서 `플랫폼 추가` 를 선택해주세요.

웹사이트 클릭 !

![웹사이트추가1]( {{ site.img_url }}/{{ page.categories }}/20170426_115302.png )

적용하려는 사이트 주소를 추가해주세요 :)

![웹사이트추가2]( {{ site.img_url }}/{{ page.categories }}/20170426_115328.png )

## 3. 로그인 버튼 만들기<a id="3-로그인-버튼-만들기" href="#3-로그인-버튼-만들기" class="s-link" aria-hidden="true"></a>

이제 기본 설정은 끝났습니다.

<https://developers.facebook.com/docs/facebook-login/web>{: target="_blank"} 여기 주소의 문서를 참고해서 연동해볼게요.

저는 로그인 버튼을 만들어서 연동해볼게요 :)

![로그인 메인]( {{ site.img_url }}/{{ page.categories }}/20170426_115457.png )

아래로 내리다보면 `플러그인 구성 도구`가 있어요.

여기서 로그인 버튼을 커스텀할 수 있는데요, 체크박스를 눌러보면 미리보기가 나오기 때문에 사용방법에 맞게 선택해주세요.

모두 선택 후 코드받기를 클릭하시면 코드가 자동생성되어 나와요.

![로그인 버튼1]( {{ site.img_url }}/{{ page.categories }}/20170426_115740.png )

앱이 여러개시라면 꼭 앱을 선택해주셔야 `앱 ID` 가 알맞게 들어가요.

![로그인 버튼2]( {{ site.img_url }}/{{ page.categories }}/20170426_115753.png )

> body 태그 닫히기 전에 넣어주세요.

```javascript
<div id="fb-root"></div>
<script>(function(d, s, id) {
    var js, fjs = d.getElementsByTagName(s)[0];
    if (d.getElementById(id)) return;
    js = d.createElement(s); js.id = id;
    js.src = "//connect.facebook.net/ko_KR/sdk.js#xfbml=1&version=v2.9&appId=★";
    fjs.parentNode.insertBefore(js, fjs);
}(document, 'script', 'facebook-jssdk'));</script>
```

> 실제로 사용할 페이스북 커스텀 버튼입니다.

```html
<div class="fb-login-button" data-max-rows="1" data-size="large" data-button-type="continue_with" data-show-faces="true" data-auto-logout-link="true" data-use-continue-as="true"></div>
```

## 4. 로그인 버튼 적용하기<a id="4-로그인-버튼-적용하기" href="#4-로그인-버튼-적용하기" class="s-link" aria-hidden="true"></a>

★ 자리에는 꼭 지금 만든 앱의 앱ID 를 넣어주셔야 해요.

간단한 예제 페이지 입니다.

> login.html

```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
</head>
<body>
    <!-- login btn -->
    <div class="fb-login-button" data-max-rows="1" data-size="large" data-button-type="continue_with" data-show-faces="true" data-auto-logout-link="true" data-use-continue-as="true"></div>

    <!-- facebook -->
    <div id="fb-root"></div>
    <script>(function(d, s, id) {
      var js, fjs = d.getElementsByTagName(s)[0];
      if (d.getElementById(id)) return;
      js = d.createElement(s); js.id = id;
      js.src = "//connect.facebook.net/ko_KR/sdk.js#xfbml=1&version=v2.9&appId=★";
      fjs.parentNode.insertBefore(js, fjs);
    }(document, 'script', 'facebook-jssdk'));</script>
</body>
</html>
```

적용해 보니 버튼이 잘 나오고있네요 !!

> 버튼 클릭시 오류가 난다면 2번에서 웹사이트를 추가해주시지 않거나 잘못 입력하신거에요 ㅠ_ㅠ

![홈페이지 적용1]( {{ site.img_url }}/{{ page.categories }}/20170426_121250.png )

![홈페이지 적용2]( {{ site.img_url }}/{{ page.categories }}/20170426_121254.png )

## 5. 앱 권한 삭제<a id="5-앱-권한-삭제" href="#5-앱-권한-삭제" class="s-link" aria-hidden="true"></a>

로그인 하면서 앱에 권한을 주게됩니다.

앱 권한은 <https://www.facebook.com/settings?tab=applications>{: target="_blank"} 에서 삭제하실 수 있습니다.

## 6. 추가 작업 (선택사항)<a id="6-추가-작업-선택사항" href="#6-추가-작업-선택사항" class="s-link" aria-hidden="true"></a>

앱 검수를 통해 기본 권한 외의 추가 권한을 얻는 경우가 있습니다.

페이스북 개발자센터의 함수를 조금 수정했습니다.

제일하단에 예제소스가 이미 있어요. 그대~로 가져다 쓰셔도 연동이 가능합니다.

우선 로그인 버튼 부분입니다.

`scope="public_profile,email,publish_pages,manage_pages"` , `onlogin="fbLogin();"` 부분이 추가되었습니다.

scope 부분은 <https://developers.facebook.com/docs/facebook-login/permissions>{: target="_blank"} 여기서 자세한 사항을 확인할 수 있습니다.

```html
<!-- login btn -->
<div class="fb-login-button" scope="public_profile,email,publish_pages,manage_pages" data-max-rows="1" data-size="large" data-button-type="continue_with" data-show-faces="true" data-auto-logout-link="true" data-use-continue-as="true" onlogin="fbLogin();"></div>
```

위의 html 부분에서 `script` 부분만 수정해볼게요.

★ 자리에는 꼭 지금 만든 앱의 앱ID 를 넣어주셔야 해요.

```javascript
function fbLogin() {
    // 로그인 여부 체크
    FB.getLoginStatus(function(response) {

        if (response.status === 'connected') {
            FB.api('/me', function(res) {
                // 제일 마지막에 실행
                console.log("Success Login : " + response.name);
                // alert("Success Login : " + response.name);
            });
        } else if (response.status === 'not_authorized') {
            // 사람은 Facebook에 로그인했지만 앱에는 로그인하지 않았습니다.
            alert('앱에 로그인해야 이용가능한 기능입니다.');
        } else {
            // 그 사람은 Facebook에 로그인하지 않았으므로이 앱에 로그인했는지 여부는 확실하지 않습니다.
            alert('페이스북에 로그인해야 이용가능한 기능입니다.');
        }
    }, true); // 중복실행방지
}

window.fbAsyncInit = function() {
    FB.init({
        appId   : '★',
        cookie  : true,
        xfbml   : true,
        version : 'v2.8'
    });
};

(function(d, s, id) {
    var js, fjs = d.getElementsByTagName(s)[0];
    if (d.getElementById(id)) return;
    js = d.createElement(s); js.id = id;
    // ko_KR 을 en_US 로 바꾸면 영문으로 로그인버튼을 사용할 수 있어요.
    js.src = "//connect.facebook.net/ko_KR/sdk.js";
    fjs.parentNode.insertBefore(js, fjs);
}(document, 'script', 'facebook-jssdk'));
```
