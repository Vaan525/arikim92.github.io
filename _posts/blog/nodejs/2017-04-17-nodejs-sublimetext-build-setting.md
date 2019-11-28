---
layout: post
comments: true
date: 2017-04-17 15:52:00
title: "Node.js Sublime Text 연동 및 빌드 세팅하기"
description: "서브라임 텍스트에서 nodejs 를 사용한다"
subject: blog
categories: [ nodejs ]
tags: [ nodejs, sublimetext ]
---

저는 맥 기준으로 설명합니다 :)

보통 윈도우는 cmd 대신에 ctrl 로 사용하면 거의 비슷합니다.

## 1. Sublime text3 설치<a id="1-Sublime-text3" href="#1-Sublime-text3" class="s-link" aria-hidden="true"></a>

[Sublime text3](https://www.sublimetext.com/3) 사이트에서 운영체제에 맞게 다운받고 설치합니다.

[Sublime text2](https://www.sublimetext.com/2) 로 설치하셔도 무방합니다.

View - Show Console 에서 아래 내용을 붙여넣기 해주세요.

> Sublime text3

```bash
import urllib.request,os,hashlib; h = ‘2915d1851351e5ee549c20394736b442’ + ‘8bc59f460fa1548d1514676163dafc88’; pf = ‘Package Control.sublime-package’; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( ‘http://packagecontrol.io/’ + pf.replace(‘ ‘, ‘%20’)).read(); dh = hashlib.sha256(by).hexdigest(); print(‘Error validating download (got %s instead of %s), please try manual install’ % (dh, h)) if dh != h else open(os.path.join( ipp, pf), ‘wb’ ).write(by)
```
> Sublime text2

```bash
import urllib2,os,hashlib; h = ‘2915d1851351e5ee549c20394736b442’ + ‘8bc59f460fa1548d1514676163dafc88’; pf = ‘Package Control.sublime-package’; ipp = sublime.installed_packages_path(); os.makedirs( ipp ) if not os.path.exists(ipp) else None; urllib2.install_opener( urllib2.build_opener( urllib2.ProxyHandler()) ); by = urllib2.urlopen( ‘http://packagecontrol.io/’ + pf.replace(‘ ‘, ‘%20’)).read(); dh = hashlib.sha256(by).hexdigest(); open( os.path.join( ipp, pf), ‘wb’ ).write(by) if dh == h else None; print(‘Error validating download (got %s instead of %s), please try manual install’ % (dh, h) if dh != h else ‘Please restart Sublime Text to finish installation’)
```

설치 후 종료(cmd + Q)하고 다시 실행시켜줍니다.

1. `Preferences - Package Control` 을 선택하시거나 `shift + cmd + p` 로 입력창을 띄웁니다.

    `add re` 까지 치시면 `Add Repository` 가 나옵니다. 엔터 눌러주시면 아래 입력창이 하나 더 나와요.

    `https://github.com/tanepiper/SublimeText-Nodejs.git` 을 입력합니다.

2. 다시 한번 `shift + cmd + p` 로 창을 띄워주시고 `install` 을 입력해주세요.

    엔터 눌러주시면 다시 창이 나오는데요, `nodejs` 라고 입력 후 제일 상단의 패키지를 설치해주세요.

3. `Tools - Build System - New Build System ...` 을 선택하면 창이 나옵니다.

    ```bash
    {
        "shell_cmd": "make"
    }
    ```

    에서

    ```bash
    {
        "cmd": ["node", "$file"],
        "file_regex": "^[ ]*File \"(...*?)\", line ([0-9]*)",
        "selector": "source.js",
        "path": "/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin:/usr/X11/bin: No such file or directory"
    }
    ```

    로 수정 후 `node-custom.sublime-build` 로 저장해주세요.

    이름은 원하는 이름으로 변경가능합니다.

4. 원하는 디렉토리에 `hello.js` 파일을 생성 후에 `console.log()` 를 작성합니다.

    `cmd + b` 를 누르면 아래와 같이 실행됩니다.

    실행이 되지 않을 시에는 `Tools - Build System - node-custom` 를 선택해 주시거나 ,

    `Tools - Build With` 로 `node-custom` 를 선택해주세요.

    ```javascript
    console.log( 'Hello World!\n' );

    // RESULT
    Hello World!

    [Finished in 0.1s]
    ```

    실행창은 `ESC` 로 닫을 수 있어요 !

5. 파일 수정은 `Preferences - Browse Packages ..` 를 선택하시면 폴더가 나옵니다.

    저희는 `User` 에 저장했기 때문에 `User` 폴더에서 파일을 찾으셔서 수정하시면 됩니다.
