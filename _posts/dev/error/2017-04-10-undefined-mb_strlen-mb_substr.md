---
layout: post
comments: true
date: 2017-04-10
title: "Uncaught Error: Call to undefined function mb_strlen().. mb_substr().."
description: "php mb_strlen, mb_substr 함수 에러"
subject: dev
categories: [ error ]
tags: [ error, php, function, strlen, substr ]
---

한글 문자열 일부를 자르려고 검색을 해서 적용을 했더니 오류가 났다.

알고보니 기본적으로 활성화 되어있지 않다고 한다.

```bash
sudo apt install php7.0-mbstring
```

아주 깔끔히 실행된다 !

하는김에 [mb_strlen, mb_substr 사용법](https://arikim92.github.io/php-mb_strlen-mb_substr)도 포스팅 해야지.

## 참고는 역시 `스택오버플로우`

- [php - Fatal error: Call to undefined function mb_strlen() - Stack Overflow](http://stackoverflow.com/questions/6419102/fatal-error-call-to-undefined-function-mb-strlen)
- [한글 번역본](https://translate.googleusercontent.com/translate_c?depth=1&hl=ko&prev=search&rurl=translate.google.com&sl=en&sp=nmt4&u=http://stackoverflow.com/questions/6419102/fatal-error-call-to-undefined-function-mb-strlen&usg=ALkJrhjHGKyE2yoa9WyABOELuD5Ytf7WBA)
