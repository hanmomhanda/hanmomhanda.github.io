---
layout: post
title: "Octopress로 GitHub에 블로그 만들기-2"
date: 2015-01-05 00:25:29 +0900
comments: true
categories: [Octopress, GitHub, blog]
---

## 새 게시물 작성/게시 큰 흐름

`octopress repo`에서 새 게시물을 작성하고 `GitHub repo`에 push해서 게시하는 큰 흐름은 다음과 같다.

1. `rake new_post[...]`로 .markdown 파일 생성
2. .markdown 파일 내용 작성
3. `rake generate`로 .markdown 파일을 .html 파일로 변환
4. `rake preview`로 미리 보기
5. `GitHub repo`에 push


## 새 게시물 파일(.markdown 파일) 생성

1탄에서 설명했지만 Octopress 블로그 게시물은 markdown 으로 작성한다.

Octopress가 markdown으로 작성된 .markdown 파일을 .html 파일로 변환할 때 markdown 파일의 물리적 위치, 파일 이름 등 여러가지 규약이 필요하며, 이를 지켜서 .markdown 파일을 작성해야 한다. 하지만 그런 규약을 하나하나 직접 신경쓸 필요는 거의 없으며, 새 게시글을 작성할 때 다음의 명령을 실행하면 알아서 처리해준다.

> rake new_post["파일명 또는 글 제목"]

![](http://i.imgur.com/zKP2W47.png)

화면에서 보는 것처럼 규약에 맞는 특정 위치에 특정 이름의 파일(source/_posts/yyyy-mm-dd-지정한파일명.markdown)을 자동으로 만들어준다. 이 파일에 새 게시물의 내용을 작성하고, `rake generate`를 실행하면 public/blog/yyyy/mm/dd/지정한파일명/index.html 파일로 변환된다.

## .markdown 파일 작성

자동 생성된 .markdown 파일은 다음과 같이 [yaml front matter](http://jekyllrb.com/docs/frontmatter/) 메타 데이타로 시작한다.

![](http://i.imgur.com/i3U7D6l.png)


yaml front matter 메타데이터를 실제 내용에 맞게 수정하고, 그 아래에 실제 게시물의 내용을 markdown 문법에 따라 작성한다.

![](http://i.imgur.com/f5smCL4.png)

## .html 파일로 변환

다음과 같이 `rake generate`를 실행하면, source/_posts/yyyy-mm-dd-지정한파일명.markdown을 Octopress가 public/blog/yyyy/mm/dd/지정한파일명/index.html 파일로 변환해준다.

![](http://i.imgur.com/ofEQFpq.png)

## 미리 보기

1탄에서 했던대로 `rake preview`를 통해 작성한 게시물을 미리 보기 할 수 있다.

![](http://i.imgur.com/6AHbQ5U.png)

![](http://i.imgur.com/msEI4Rj.png)

## GitHub에 deploy

미리 보기를 통해 내용 최종 확인을 마치면 GitHub에 deploy 한다.

이번에는 1탄에서 소개했던 첫 번째 방법인 `rake deploy` 대신 두 번쨰 방법인 git 명령을 직접 실행해서 deploy 해본다.

`rake generate`로 public 폴더에 블로그 내용이 생성되었으므로, public 폴더의 내용을 `deploy repo`가 있는 \_deploy 폴더로 복사하고, \_deploy 폴더에서 git 명령으로 GitHub에 push 하면 된다.

![](http://i.imgur.com/DZB32Fj.png)

마지막으로 `git push`를 실행하고, GitHub 계정 정보를 입력해서 `GitHub repo`에 push 한다.

![](http://i.imgur.com/ngtLG0x.png)

블로그 URL을 주소창에 입력하여 접속하면 첫 번째 게시물을 확인할 수 있다.

![](http://i.imgur.com/9rTQr7q.png)


----------

2탄까지가 Octopress로 GitHub에서 블로그를 운영하는데 필요한 최소한의 내용이다.

3탄에서는 가볍게 블로그 Title, SubTitle, Footer 등을 매만져보자.