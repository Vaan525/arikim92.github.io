---
layout: post
comments: true
date: 2019-04-09
title: "슬랙 앱 만들기"
description: "내 스타일로 슬랙 앱 만들기"
subject: blog
categories: [ chatbot ]
tags: [ chatbot, slack ]
---

# 슬랙 앱 만들기

## 참고 URL

- 슬랙 홈페이지 <https://arikim.slack.com/home>{: target="_blank"}

- 슬랙 API <https://api.slack.com/>{: target="_blank"}


## 1. 봇 만들기

<https://api.slack.com/apps>{: target="_blank"} 에서 `Create New App` 을 선택합니다.

`App Name` 과 `Workspace` 를 선택합니다.

`App Name` 은 추후에 바꿀 수 있어요 ㅎ_ㅎ


## 2. [봇 기본 세팅](https://api.slack.com/apps/{슬랙_키}?created=1){: target="_blank"}

> Display Information

![봇 이름 세팅]( {{ site.img_url }}/{{ page.categories }}/create-slack-app01.png )

우선 아래에 `Display Information` 을 작성하고 `Save Change` 로 저장합니다.

이름과 설명, 아이콘 을 설정할 수 있어요.

앱을 제출하려면 [가이드라인](https://api.slack.com/docs/slack-apps-guidelines){: target="_blank"} 에 따라서 설정해주세요.

> Building Apps for Slack

그 다음은 `Building Apps for Slack` 에 나온 순서대로 진행하면 됩니다.


## 3. 봇 세팅

> Features - Bot Users

이름을 정해주고 `Add Bot User` 로 저장합니다.

> Features - Event Subscriptions - Enable Events

이벤트 관련한 문서는 <https://api.slack.com/events-api>{: target="_blank"} 여기를 참고하시면 됩니다.

`Enable Events` 를 활성화 시켜줍니다.

`Request URL` 에 서버 주소를 입력합니다. 서버에 별 세팅을 안하고 켜 놓기만 했어요.

![Request URL Fail]( {{ site.img_url }}/{{ page.categories }}/create-slack-app02.png )

`Your URL didn't respond with the value of the challenge parameter.` 과 같은 에러가 났네요 .. 

```javascript
console.log( "[ req.body ]", req.body );
````

```bash
2019-04-09 12:54:59 POST /slack
[ req.body ] {
    "token": "*************************",
    "challenge": "****************************************************",
    "type": "url_verification"
}
```

받은 `challenge` 를 그대로 넘겨주는 소스코드를 상단에 넣었어요.

참고 URL: <https://api.slack.com/events/url_verification>{: target="_blank"}

```javascript
// 슬랙 인증
if ( req.body.challenge && req.body.type == "url_verification" ) {
    res.json({ challenge: req.body.challenge });
}
```

성공 :)

![Request URL Success]( {{ site.img_url }}/{{ page.categories }}/create-slack-app03.png )

> Features - Event Subscriptions - Subscribe to Bot Events

받아볼 이벤트를 정합니다. 아래 내용 이외에 추가할 내용은 추가 설명이 나와있으니 참고하시면 됩니다 :)

`Add Bot User Event` 버튼으로 아래 4가지를 추가해줍니다.

- message.im

- message.groups

- message.channels

- im_created

추가하고 `Save Changes` 를 꼭 눌러주세요!

> Features - OAuth & Permissions - Redirect URLs

저는 Event 받아보는거와 똑같이 입력했어요.

> Features - OAuth & Permissions - Scopes

`chat:write:user` 는 메세지를 보내려면 필수에요.

더 필요한 내용을 추가하면 돼요 :)

![scope list]( {{ site.img_url }}/{{ page.categories }}/create-slack-app06.png )

> Settings - Basic Infomation - Building Apps for Slack - Install your app to your workspace

여기까지 오셨다면! 4개 완료했어요!

![중간점검]( {{ site.img_url }}/{{ page.categories }}/create-slack-app04.png )

`Install App to Workspace` 버튼을 눌러주면 권한을 체크하고 슬랙에 봇이 추가됩니다.


## 4. 슬랙에서 대화

![슬랙에 추가된 봇]( {{ site.img_url }}/{{ page.categories }}/create-slack-app05.png )

```bash
=====================================
2019-04-09 17:08:50 POST /slack
2019-04-09, Tue 17:08:50 [ req.body ] {
    "token": "**********************",
    "team_id": "**********",
    "api_app_id": "**********",
    "event": {
        "client_msg_id": "************************************",
        "type": "message",
        "text": "안녕!",
        "user": "**********",
        "ts": "1554797330.000700",
        "channel": "**********",
        "event_ts": "1554797330.000700",
        "channel_type": "im"
    },
    "type": "event_callback",
    "event_id": "*********",
    "event_time": 1554797330,
    "authed_users": [
        "**********"
    ]
}
2019-04-09, Tue 17:08:53 
=====================================
2019-04-09 17:08:53 POST /slack
2019-04-09, Tue 17:08:53 [ req.body ] {
    "token": "**********************",
    "team_id": "**********",
    "api_app_id": "**********",
    "event": {
        "client_msg_id": "************************************",
        "type": "message",
        "text": "안녕!",
        "user": "**********",
        "ts": "1554797330.000700",
        "channel": "**********",
        "event_ts": "1554797330.000700",
        "channel_type": "im"
    },
    "type": "event_callback",
    "event_id": "*********",
    "event_time": 1554797330,
    "authed_users": [
       "**********"
    ]
}
```