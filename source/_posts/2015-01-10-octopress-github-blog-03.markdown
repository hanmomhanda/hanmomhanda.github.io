---
layout: post
title: "Octopress로 GitHub에 블로그 만들기-3"
date: 2015-01-10 13:10:00 +0900
comments: true
categories: [Octopress, GitHub, blog]
---

## _config.yml

블로그 전반적인 설정 정보는 `octopress repo/_config.yml`에서 수정할 수 있다.

설정 내용은 크게 세 가지로 카테고리로 나누어져 있다. 각 카테고리 별 세부 설정 정보는 파일 안에 주석으로 잘 설명되어 있다. 

- Main Configs

    url, title, subtitle, author, 검색, 사이트 설명 등 블로그 정보 설정

- Jekyll & Plugins

    블로그 게시물 publishing을 위한 설정

- 3rd Party Settings
    
    `Github`, `페이스북 좋아요`, `Google Plus +1`, `트위터`, `Disqus` 등 써드 파티 애플리케이션과의 연계 설정

## Main Configs

기본으로 설정되어 있는 블로그는 아래와 같은데, 블로그 제목, 부제목 등의 header 와 블로그 저자명이 있는 footer 를 변경해보자.

### 변경 전

#### _config.yml

![](http://i.imgur.com/7iAT4tq.png)

#### 블로그

![](http://i.imgur.com/lcaf3BQ.png)

![](http://i.imgur.com/CDRbsoS.png)

### 변경 후

#### _config.yml

![](http://i.imgur.com/biP4wij.png)

`_config.yml` 파일 수정 후 `rake preview`로 미리 보기한다(`rake preview`를 실행하면 `rake generate`도 실행된다).

#### 블로그 미리 보기

![](http://i.imgur.com/Pz4RavG.png)

![](http://i.imgur.com/nuaxn0z.png)

### GitHub에 Deploy

[2탄](http://hanmomhanda.github.io/blog/2015/01/05/octopress-github-blog-02/) 내용을 참고해서 `public` 폴더의 내용을 `_deploy` 폴더로 복사하고, `_deploy` 폴더에서 `git add`와 `git commit`을 실행하고 `git push origin master`로 GitHub에 Deploy 한다.

블로그 URL에 접속하면 아래와 같이 블로그 제목 등이 변경된 것을 확인할 수 있다.

![](http://i.imgur.com/ZBiu0Tp.png)


----------
이제 `Octopress`로 블로그를 운영하는 큰 틀은 모두 돌아봤다.

4탄에서는 폰트 변경, 소스 코드 쪼가리(code snippet) 넣기, 블로그 내용 일부만 먼저 보여주기 등을 다뤄본다.

