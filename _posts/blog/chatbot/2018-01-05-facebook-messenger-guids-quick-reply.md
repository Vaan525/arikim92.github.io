---
layout: post
comments: true
date: 2018-01-05 14:15:00
title: "페이스북 메신저 챗봇 가이드 - 1편 Quick Reply"
description: "Quick Reply 챗봇에서 사용하기"
subject: blog
categories: [ chatbot ]
tags: [ chatbot, facebook, facebook-messenger ]
---

1편이 Quick Reply 인 이유는 제가 이 부분을 공부했기 때문입니다 (..)

페이스북 문서 [https://developers.facebook.com/docs/messenger-platform/send-messages/quick-replies](https://developers.facebook.com/docs/messenger-platform/send-messages/quick-replies) 를 참고하시면 `더욱` 편리합니다.

빠른 버튼은 아래에 기본 제공되는 버튼이 아니라 해당 메뉴를 실행했을 경우에만 확인할 수 있습니다.

## 1. 텍스트 빠른 답장<a id="1-텍스트-빠른-답장" href="#1-텍스트-빠른-답장" class="s-link" aria-hidden="true"></a>

아래는 영화퀴즈를 풀 수 있는 영화퀴즈챗봇 무무 이미지 입니다.

`OX 퀴즈` 버튼을 선택하면 O 와 X 를 선택할 수 있는 퀵 버튼이 나오게 됩니다.

보이는 바와 같이 텍스트 or 이모티콘도 설정 가능합니다.

> [영화퀴즈챗봇 무무](https://m.me/moviequizbot)

![영화퀴즈챗봇무무]( {{ site.img_url }}/{{ page.categories }}/facebook-messenger-guids-quick-reply01.jpeg )

![영화퀴즈챗봇무무]( {{ site.img_url }}/{{ page.categories }}/facebook-messenger-guids-quick-reply02.jpeg )

## 2. 위치 빠른 답장<a id="2-위치-빠른-답장" href="#2-위치-빠른-답장" class="s-link" aria-hidden="true"></a>

퀵 버튼으로 위치정보도 보낼 수 있습니다.

메르세데스 벤츠 코리아 챗봇에서는 `가까운 전시장`을 찾아주는 기능이 있습니다.

> Mercedes-Benz Korea 챗봇

![MercedesBenzKorea]( {{ site.img_url }}/{{ page.categories }}/facebook-messenger-guids-quick-reply03.jpeg )

## 3. 코드<a id="3-코드" href="#3-코드" class="s-link" aria-hidden="true"></a>

```javascript
/*
 * 모든 내용은 사전 작업이 필요하고 아래 코드는 일부분입니다.
 *
 * senderID : 답장을 받을 ID
*/
```

> 2번째 이미지 예시

```javascript
...

let sendData = {
    recipient: { id: senderID },
    message: {
        text: '답 : X',
        quick_replies: [{
            content_type: "text",
            title: "메뉴" ,
            payload: "quick_menu"
        }, {
            content_type: "text",
            title: "다음 퀴즈"  ,
            image_url: "http://example.com/img/rabbit.png",
            payload: "quick_next_quiz"
        }]
    }
};

...
```

> 3번째 이미지 예시

```javascript
...

let sendData = {
    recipient: { id: senderID },
    message: {
        text: '현재 위치를 알려주시면 가까운 전시장을 안내해드릴께요.',
        quick_replies: [{
            content_type: "location"
        }]
    }
};

...
```

> 2번째 이미지 결과

위와 같이 제공된 퀵 버튼을 누르면 아래와 같이 응답이 옵니다.

`메뉴` 퀵 버튼을 눌러서 `payload`, `text` 가 메뉴로 넘어왔네요.

```bash
{
    "sender": {
        "id": "sender_id"
    },
    "recipient": {
        "id": "recipient_id"
    },
    "timestamp": 1515479120546,
    "message": {
        "quick_reply": {
            "payload": "quick_menu"
        },
        "mid": "mid.$cAAgU6J_dh4",
        "seq": 123,
        "text": "메뉴"
    }
}
```

> 3번째 이미지 결과

`message.attachments.title` 은 위치를 움직이면 `Pinned Location` 으로 ,

자신의 위치를 보낸다면 `Gildong's Location` 으로 응답이 옵니다.

스마트폰으로 본다면 안드로이드는 구글맵, 아이폰은 애플맵, 컴퓨터는 Bing맵으로 보여줍니다.

`lat` 와 `long` 으로 정확한 위치도 알 수 있습니다.

```bash
{
    "sender": {
        "id": "sender_id"
    },
    "recipient": {
        "id": "recipient_id"
    },
    "timestamp": 1515478660248,
    "message": {
        "is_echo": true,
        "app_id": 'app_id',
        "mid": "mid.$cAAgUzzZBPr",
        "seq": 1234,
        "attachments": [{
            "title": "Pinned Location",
            "url": "https://l.facebook.com/l.php?u=https%3A%2F%2Fwww.bing.com%2Fmaps%2Fdefault.aspx%3Fv%3D2%26pc%3DFACEBK%26mid%3D8100%26where1%3D37.551768827203%252C%2B126.92533229794%26FORM%3DFBKPL1%26mkt%3Den-US&h=ATPj4VN14nslJBMIU0XSsreQIOpI8gB7C3JM46MlcchwGUM1j22lqh2QTbG1X-DM8kbB0Bm58CNIB3B5qdkuex4PXxDJOqJM5POZhteGGamadr1-5Q&s=1&enc=AZP7PoiCa93kbTu4Z7gxjj5zYcdz8SJTuu1R5QqC1h1tgx6dMRsgunOSuTDYLZ90QTjc0KWyVydf_RXAfL_f5qBi",
            "type": "location",
            "payload": {
                "coordinates": {
                    "lat": 37.551768827203,
                    "long": 126.92533229794
                }
            }
        }]
    }
}
```

제가 홍대로 pin 을 찍었습니다.

`message.attachments.url` 은 이렇게 보입니다.

![위치보내기]( {{ site.img_url }}/{{ page.categories }}/facebook-messenger-guids-quick-reply04.png )


## 4. 다음이야기<a id="4-다음이야기" href="#4-다음이야기" class="s-link" aria-hidden="true"></a>

다음엔 천천히 템플릿에 대해서 알아볼게요 :)
