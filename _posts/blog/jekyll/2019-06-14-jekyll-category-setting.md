---
layout: post
comments: true
date: 2019-06-14
title: "Github Page Jekyll 에 카테고리 추가하기"
description: "지킬에 카테고리 설정하기"
subject: blog
categories: [ jekyll ]
tags: [ jekyll ]
---

## 1. Post 에서 카테고리 추가하기

카테고리도 여러가지 방법으로 추가할 수 있어요.

저는 여러가지 방법을 시도하다가 아래처럼 정착했어요.

```markdown
---
layout: post
comments: true
date: 2019-06-14
title: "Github Page Jekyll 에 카테고리 추가하기"
description: "지킬에카테고리 설정하기"
subject: blog
categories: [ jekyll ]
tags: [ jekyll ]
---
```

배열도 가능하고 텍스트도 가능해요.

```
category: 텍스트
categories: [ 배열 ]
```

## 2. Category 폴더 만들기

카테고리는 혼자 모든 리스트를 출력해주지 않아요 ㅠ_ㅠ

따로 config 파일에 변수로 설정해줄게요.

큰 depth 가 늘어나면 하나씩 수정해줘야 하지만.. 자주 생기거나 수정하지 않으니까 괜찮아요 (?)

> _config.yml
 
```yml
category_list: [ nodejs, javascript, tip, diary, linux, chatbot, php ,publishing, jekyll, sql, error ]
```

제일 상단에 `category` 폴더를 추가해주세요.

`{foldername}` 으로 폴더를 추가하고 `index.html` 이나 `index.md` 를 만들면 `/{foldername}` 으로 Url 이 생성돼요.

`category/index.html` 을 만들면 `/category` 로 Url 이 생성되는거에요!

개별 카테고리 리스트를 위해서 각각 파일로 만들어줬어요.

![category-folder]( {{ site.img_url }}/{{ page.categories }}/jekyll-category-setting01.png )

index 의 확장자가 html 인 이유는m 아래 파일 내용이 md 파일 일 때 동작하지 않아서 html 로 바꿔줬어요.

`permalink` 는 Url 을 직접 설정할 수 있는 태그에요. 동작하지 않을 때 넣어주세요.

( 저는 원래 폴더 위치가 다른곳이여서 아직 남아있네요 ㅎㅎ )

- 전체 카테고리 리스트

> category/index.html

```html
---
layout: default
permalink: '/category'
---

<div class="category-wrap">
{% for list in site.category_list %}
    <h1 class="category-title"><a href="/category/{{ list }}">{{ list | upcase }}</a></h1>
    <ul class="posts-list">
        {% for post in site.categories[ list ] %}
        <li>
            <h3>
                <a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a>
                <small>{{ post.date | date_to_string }}</small>
            </h3>
        </li>
        {% endfor %}
    </ul>
{% endfor %}
</div>
```

`site.category_list` 는 `_config.yml` 파일에서 설정한 저의 변수 이름이에요.

`list` 라는 변수에 제가 설정한 배열을 담아서 `for` 문을 사용해요.

- 개별 카테고리 리스트

> _layouts/category.html

```html
---
layout: default
---

<div class="catalogue">
    <h1 class="category-title"><a href="/category/{{ page.title }}">{{ page.title }}</a></h1>
    {% assign cate = page.category | default: page.title %}
    {% for post in site.categories[ cate ] %}
    <a href="{{ post.url | prepend: site.baseurl }}" class="catalogue-item">
        <div>
            <time datetime="{{ post.date }}" class="catalogue-time">{{ post.date | date: "%B %d, %Y" }}</time>
            <h1 class="catalogue-title">{{ post.subject | upcase }}/ {{ post.title }}</h1>
            <h4 class="catalogue-desc">{{ post.description }}</h4>
            <div class="catalogue-line"></div>
            <p class="catalogue-content">{{ post.content | strip_html | truncatewords: 30 }}</p>
        </div>
    </a>
    {% endfor %}
</div>
```

> category/chatbot.md

```markdown
---
layout: category
title: CHATBOT
category: chatbot
permalink: '/category/chatbot'
---
```

category.html 에서 page.title or page.category 로 해당 카테고리 리스트를 불러오고 있어요.

`site.categories.chatbot` 은 정상동작 하는데 `site.categories[ page.title ]` 은 적용이 안되는거에요!!

확인해보니 `page.title` 은 제가 대문자로 쓰고싶은데 대문자는 적용이 안되더라구요 ㅠㅠ

그래서 `category` 에 소문자로 한 번 더 적어줬어요 ...ㅎㅅㅎ

`layout`, `permalink` 외에는 선택사항으로 적어주시면 돼요 :)

![category-folder]( {{ site.img_url }}/{{ page.categories }}/jekyll-category-setting02.png )

![category-folder]( {{ site.img_url }}/{{ page.categories }}/jekyll-category-setting03.png )