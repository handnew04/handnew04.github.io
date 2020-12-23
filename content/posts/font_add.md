---
title: "[Hugo] Hugo git블로그 폰트 추가하기"
date: 2019-04-04T18:29:41+09:00
tags: ["Hugo","github" ]
keywords: ["font","gitpage","hugo","폰트"]
description: "hugo theme 중 natrium 테마를 기준으로 작성하였습니다."
draft: false
---


> hugo theme 중 natrium 테마를 기준으로 작성하였습니다.

*****

기존의 글 내용을 보여주는 폰트가 한글지원이 되지 않아서 나눔고딕폰트로 변경하였다.
인터넷에서 무료로 나눔고딕 폰트를 다운로드 할 수 있다. [*다운로드*](https://hangeul.naver.com/download.nhn)

나눔고딕 폰트를
**블로그 > themes > 테마이름 > static > fonts** 에 넣고 
static 의 font.css 에 아래 코드를 추가하였다.

```
@font-face {
  font-family: 'Nanum-Gothic';
  font-style: normal;
  font-weight: 400;
  src: url('../fonts/Nanum-Gothic.ttf') format('truetype');
}
```
그 후,
static 의 main.css 파일에서 본문(body) 등의 font-family 에 Nanum-Gothic 을 추가하였다.

```
body {
  font-family: 'Nanum-Gothic', 'Merriweather', serif;
  -webkit-hyphens: auto;
  hyphens: auto;
}
```
