---
layout: post
comments: true
date: 2019-06-07 18:27:00
title: "Github Page Jekyll-paginate 사용하기 및 참고"
description: "Github Page Pagination 설치없이 사용법 및 참고"
subject: blog
categories: [ jekyll ]
tags: [ jekyll, plugin ]
---

## 참고

공식 홈페이지: <https://jekyllrb-ko.github.io/docs/pagination/>

Github Page 에서는 설치없이 pagination 사용이 가능해요.

하지만 2를 사용하려고 찾아보던중, 2는 설치만 가능하구요!

pagination 자체는 index.html 외에는 동작하지 않는다고 해요 ㅠㅠ

다른 Url 로 옮기려고 했는데 안되더라구요 ㄷㄷ


## 사용법

> _config.yml
 
```yml
plugins:
  - jekyll-paginate
```

> list.html

```html
<div class="pagination">
    {% if paginator.previous_page %}
        <a href="{{ paginator.previous_page_path | prepend: site.baseurl }}" class="fas fa-chevron-left"></a>
    {% endif %}
    {% if paginator.next_page %}
        <a href="{{ paginator.next_page_path | prepend: site.baseurl }}" class="fas fa-chevron-right"></a>
    {% endif %}
    
    <span class="page-left">{{ paginator.page }}</span><span class="page-slice"> / </span><span class="page-right">{{ paginator.total_pages }}</span>
</div>
```

빨간색 네모처럼 만들어서 사용할 수 있다 :)

![미리보기-이미지]( {{ site.img_url }}/{{ page.categories }}/jekyll-paginate-plugin-pagination01.png )