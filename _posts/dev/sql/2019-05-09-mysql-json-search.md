---
layout: post
comments: true
date: 2019-05-09
title: "MySQL JSON 검색하기"
description: "json 타입의 컬럼 데이터 내에서 검색하기"
subject: dev
categories: [ sql ]
tags: [ sql, mysql, json, search ]
---

# MySQL JSON 검색하기

json 검색하는 법을 검색했는데 이것저것 나와있어서 불편했어요 (..)

저는 정말 검색하는 법만 알려 드릴게요 (?!)

공식 홈페이지도 같이 참고하면 좋을 것 같아요 :)

[MySQL :: MySQL 5.7 Reference Manual :: 11.6 The JSON Data Type](https://dev.mysql.com/doc/refman/5.7/en/json.html){: target="_blank"}

User Table 에서 `user_data` 를 object 로 담아서 기본 내용 외에 필요한 내용을 저장하고 있어요.
오늘 예제는 `핸드폰 번호` 와 `우리집맛집 금정점` 을 찾아 볼게요 :)

> example)

```json
{
    "info": {
        "phone": "01012345678",
        "certification": true,
        "store_info": [{
            "employer": "홍길동",
            "store_name": "우리집맛집 천호점"
        }, {
            "employer": "홍길동",
            "store_name": "우리집맛집 합정점"
        }, {
            "employer": "홍길동",
            "store_name": "우리집맛집 금정점"
        }]
    }
}
```

!!! `info` 검색 방법은 많은데 이중으로 더 깊은 내용을 검색하는 방법은 잘 안 나와 있더라구요 ㅠ_ㅠ
우선 `info` 를 찾아 볼게요.

```sql
select JSON_EXTRACT( user_data, '$.info' ) from user_t where uuid = 1;
```

[Result](https://www.notion.so/455c92d5493c4d6e93497f29b7456f62)

음 .. 설마 ? 하고 찍어 봤어요. 

```sql
select JSON_EXTRACT( user_data, '$.info.phone' ) from user_t where uuid = 1;
```

[Result](https://www.notion.so/d0312a855f3d4c3296b20bdc3dd027fb)

아주 쉽게 성공했어요 하하하ㅏㅏㅏㅏ
`as` 를 사용해서 이름을 바꿔볼께요.

```sql
select JSON_EXTRACT( user_data, '$.info.phone' ) as phone from user_t where uuid = 1;
```

[Result](https://www.notion.so/05df748e96a6467c91abad94058a280f)

하지만 `phone` 으로 조건문을 걸면 에러가 나요 ..

```sql
Unknown column 'phone' in 'where clause'
```

조건은 원래 넣었던 함수를 사용해서 넣어주면 제대로 작동해요 ^-^/

```sql
select JSON_EXTRACT( user_data, '$.info.phone' ) as phone from user_t
where uuid = 1 and JSON_EXTRACT( user_data, '$.info.phone' ) = "01012345678";
```

[Result](https://www.notion.so/9044f32ea7544f16b8f93bafdc1432ff)

핸드폰 번호는 찾았으니 `우리집맛집 금정점` 을 찾아요!
`store_info` 는 배열 이기 때문에 번호로 접근이 가능해요.
`우리집맛집 금정점` 은 1번 이니까 1번으로 접근 할게요.

```sql
select JSON_EXTRACT( user_data, '$.info.store_info[ 1 ].store_name' ) as store_name
from user_t where uuid = 1;
```

[Result](https://www.notion.so/a303134696864cc5b3062ca2b9906939)

`JSON_EXTRACT` 함수 하나만으로 모든 json 검색이 가능해졌어요!
`$.` 이후로 object 접근 하듯이 그대로 써주면 되네요 :)