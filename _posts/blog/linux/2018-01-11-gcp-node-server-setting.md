---
layout: post
comments: true
date: 2018-01-11 12:30:00
title: "Google Cloud Platform 에서 node.js 서버 세팅하기"
description: "GCP 에서 node 서버 세팅하는 내가 제일 보고싶은 포스팅"
subject: blog
categories: [ linux ]
tags: [ ubuntu, nodejs, server ]
---

사실 어느정도 세팅이 되어있는 상태에서 쓰기때문에 양해 부탁드려요.

## 1. 준비작업<a id="1-준비작업" href="#1-준비작업" class="s-link" aria-hidden="true"></a>

Google Cloud Platform 에 가입하셔서 프로젝트를 만들어주세요.

서버가 있어야 진행이 되니까요 ...?

아래와 같은 URL 로 들어가시면 `VM인스턴스`를 만들 수 있습니다.

> https://console.cloud.google.com/compute/instances?project=[프로젝트명]

![VM메인]( {{ site.img_url }}/{{ page.categories }}/gcp-npm-server-setting01.png )

## 2. 인스턴스 만들기<a id="2-인스턴스-만들기" href="#2-인스턴스-만들기" class="s-link" aria-hidden="true"></a>

![VM설정]( {{ site.img_url }}/{{ page.categories }}/gcp-npm-server-setting02.png )

이름은 자유롭게 지어주세요.

영역 부분입니다. 저는 서버를 미국에 뒀는데요, `Facebook chatbot` 작업을 할 거라서 그쪽에 뒀어요.

[영역 참고자료](https://cloud.google.com/compute/docs/regions-zones/?hl=ko&_ga=2.216688213.-2101340162.1498636459) 에 가시면 자세히 볼 수 있어요.

한국과 제일 가까운 서버를 선택하시려면 일본에 있는 `asia-northeast1` 를 선택하시면 됩니다.

머신 유형에서는 제일 작은 초소형을 선택했어요.

그렇게 많은 서비스를 돌릴것도 아니고 공부용이거든요 ㅎㅎ

부팅 디스크는 Ubuntu 로 사용하려고 Ubuntu 를 선택했습니다.

기타 설정들은 `물음표`를 눌러서 참고하시면 됩니다.

컴퓨터에 대한 어느정도 지식이 있으면 선택하기 쉬우실거에요 !

## 3. 인스턴스 접속<a id="3-인스턴스-접속" href="#3-인스턴스-접속" class="s-link" aria-hidden="true"></a>

![VM메인]( {{ site.img_url }}/{{ page.categories }}/gcp-npm-server-setting01.png )

인스턴스 메인화면으로 나와서 연결 부분에 SSH 접속을 할 수 있어요.

다른방법으로 저는 맥에서 `nodejs.command` 라는 파일을 만들어서 사용합니다.

```bash
#!/bin/sh
gcloud compute --project "[프로젝트명]" ssh --zone "[영역]" "[계정]@[인스턴스 이름]"
```

으로 저장하면 바로 접속이 가능해요 !

## 4. 서버세팅<a id="4-서버세팅" href="#4-서버세팅" class="s-link" aria-hidden="true"></a>

작업을 좀 쉽게하기 위해 슈퍼관리자로 변신합니다.

```bash
# sudo su
```

> 업그레이드

아래 두 작업은 시간이 좀 걸립니다.

그래도 업그레이드는 필수 !

```bash
# apt update
# apt dist-upgrade
```

> nginX 설치

서버 작업을 위해 nginx 를 설치합니다.

```bash
# apt install nginx
```

> node 설치

```bash
# apt install npm
```

n 은 node 의 버전을 쉽게 할 수 있는 프로그램입니다.
`n help` 로 사용법을 볼 수 있습니다.

```bash
# npm install -g n
```

`n ls` 로 설치된 버전을 확인할 수 있습니다.

`n lts` 를 설치하고 안정버전을 설치합니다.

```bash
# n lts
->  install : node-v8.9.4
    mkdir : /usr/local/n/versions/node/8.9.4
    fetch : https://nodejs.org/dist/v8.9.4/node-v8.9.4-linux-x64.tar.gz
######################################################################## 100.0%
    installed : v8.9.4

# n stable
->  install : node-v9.4.0
    mkdir : /usr/local/n/versions/node/9.4.0
    fetch : https://nodejs.org/dist/v9.4.0/node-v9.4.0-linux-x64.tar.gz
######################################################################## 100.0%
    installed : v9.4.0
```

`node -v` 로 현재 설정된 버전을 확인할 수 있습니다.

```bash
# node -v
-> v9.4.0
```

## 5. nodejs 테스트<a id="5-nodejs-테스트" href="#5-nodejs-테스트" class="s-link" aria-hidden="true"></a>

node 설치까지 완료되었으니 이제 테스트를 해볼까요 ?

`node` 입력 후 엔터를 치면 바로 사용할 수 있어요.

```bash
root@nodejs:/home/ubuntu# node
> console.log('test'); // 입력
test // 결과
undefined
> // 멈추고 싶을 땐 control + C 를 2번 입력합니다.
(To exit, press ^C again or type .exit)
> 
root@ari-node:/home/ubuntu# 
```

![설명]( {{ site.img_url }}/{{ page.categories }}/gcp-npm-server-setting03.png )

파일을 만들어 사용도 가능합니다.

```bash
# cd /home/ubuntu
# mkdir nodejs
# cd nodejs
# vi test.js
# i // vi 의 입력모드
# console.log('node.js');
# esc + :wq // 입력모드 종료 후 파일을 저장
# node test.js

root@ari-node:/home/ubuntu/nodejs# node test.js
node.js // 결과
```

여기까지 입니다 :)