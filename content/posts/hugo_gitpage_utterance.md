---
title: "[Hugo] Hugo gitpage utterances 댓글달기"
date: 2019-04-04T18:12:45+09:00
tags: ["Hugo", "github"]
keywords: ["utterances", "hugo", "댓글", "gitpage"]
description: "post, 즉 글을 쓸 때 마다 밑에 댓글입력칸이 보여야 했기에 테마 내부에 글의 레이아웃으로 쓰는 파일이 있을거라 생각했다."
draft: false
---


> *이 블로그는 hugo를 이용하여 만들어진 블로그입니다.*<br>
> *블로그에 댓글기능을 달기위하여*<br>
> *[utterances](<https://github.com/utterance>) 를 사용하였습니다.*<br>
> *hugo theme 중 [natrium](https://github.com/mobybit/hugo-natrium-theme/) 테마를 기준으로 글을 작성하였습니다.*<br>

***

[*참고블로그*](https://astrod.github.io/etc/2018/05/28/utterances-%EC%A0%81%EC%9A%A9/) 를 보고 진행하였는데,
블로그 내부에 어느부분에 코드를 삽입해야될지 알수가 없었다. 

post, 즉 글을 쓸 때 마다 밑에 댓글입력칸이 보여야 했기에 테마 내부에 글의 레이아웃으로 쓰는 파일이 있을거라 생각했다.

**자신의hugo블로그 > themes > 자신의테마 > layouts > _default > single.html** 에서 찾을 수 있었다.

```
</main>

<script src="https://utteranc.es/client.js"
        repo="handnew04/blog-comments"
        issue-term="pathname"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

{{ partial "footer.html" . }}

```

footer.html 이 시작되기전, 본문이 끝난 아랫부분에 코드를 삽입하였다. 
