---
layout: post
title: "Octopress로 GitHub에 블로그 만들기-1"
date: 2015-01-04 20:27:37 +0900
comments: true
categories: [Octopress, GitHub, blog]
---

새해 맞이 프로젝트 중 하나로 블로그를 운영해보려 한다.

네이버나 구글 등에서 제공하는 블로그 서비스를 이용하거나 워드프레스를 이용해서 만드는 방법도 있겠지만, 주로 개발 관련 공부 내용을 정리하고 공유하는 목적이라 다음과 같은 요건이 필요했다.

> 예쁜 Syntax Highlight

> 귀찮은 설치형은 가급적 배제

> markdown으로 빠르고 쉽게 블로그 작성

> 깨알 같은 플러그인 기능이 있다면 금상첨화

찾아보니 Static Site Generator라는 게 있더라~

https://www.staticgen.com/, https://staticsitegenerators.net/, http://mashable.com/2014/08/28/static-website-generators/ 를 참고해서 [Octopress](http://octopress.org/)를 사용하기로 했다.

Octopress는 GitHub, Heroku, Rsync 호스팅을 지원하는데 Rsync는 잘 모르겠고, GitHub 과 Heroku 중에서 선택하기 위해 검색을 하다가 https://bigdatatools.wordpress.com/2013/08/05/octopress-on-heroku-vs-github/ 를 보고 GitHub로 하기로 했다. 글에 따르면 Heroku는 다음과 같은 단점이..

> 트래픽이 증가하면 Dyno를 추가해야 한다. <- Dyno는 뭐냐..

> Heroku의 가상 머신은 웹 페이지에 1시간 동안 접속이 없으면 sleep mode가 되고, sleep mode 인 상태에서 누군가 접속하면 페이지 로딩에 시간이 좀 걸린다. <- 치명적이다..

> Heroku는 SSH Key를 Dropbox 같은 걸로 공유하지 않으면 여러 PC에서 작업을 할 수가 없다. <- 치명적이다..(2)

결국 Octopress와 GitHub의 조합으로 블로그를 만들기로 했다.

Octopress로 GitHub에 블로그를 만드는 큰 그림은 다음과 같다.

- octopress를 로컬에 clone하고(로컬에 clone한 repo를 앞으로 `octopress repo`라 한다)

- `octopress repo` 내에서 이런저런 설정을 하고

- GitHub의 Repository를 `octopress repo`의 remote로 설정

- `octopress repo` 내의 source 폴더 내에서 규약에 맞게 포스팅 할 블로그 파일(.markdown 파일) 작성

- `octopress repo`를 remote로 push하면 GitHub의 Page 기능을 통해 블로그 내용이 웹 페이지로 반영

큰 그림을 대략 머리에 넣어두고 Octopress로 GitHub에 블로그를 만들어보자.

앞으로 나오는 모든 내용은 [Linux Mint](http://www.linuxmint.com/) 17 Qiana 에서 실행한 내용이다.

Octopress에서도 [설정 방법](http://octopress.org/docs/setup/)을 간단 명료하게 잘 만들어놨으니 참고하자.

## 사전 설치 내용

1. Git 설치

    Octopress는 Git을 기반으로 작동하며, GitHub를 이용하려면 당연히 Git가 필요하다.
    Git의 설치는 http://www.git-scm.com/ 참조

2. Ruby 1.9.3+ 설치

    Ruby는 잘 모르지만 Octopress의 설치 매뉴얼에 따르면 rbenv 와 RVM 두 가지 방법으로 Ruby의 설치가 가능한데, RVM이 더 간단해보여 여기서는 RVM으로 진행한다.

    - RVM 설치

        > curl -L https://get.rvm.io | bash -s stable &#45;&#45;ruby

        처음 실행하면 아래와 같이 signature 관련 에러 발생하는데

        ![](http://i.imgur.com/PJ5MakW.png)

        화면에 안내된대로 아래의 명령을 수행하면 해결된다.

        > gpg &#45;&#45;keyserver hkp://keys.gnupg.net &#45;&#45;recv-keys #######

        다시 아래의 명령 실행

        > curl -L https://get.rvm.io | bash -s stable &#45;&#45;ruby

        ![](http://i.imgur.com/GmoNNol.png)

        ![](http://i.imgur.com/ozqAHGM.png)

        > sudo 비번 입력

        나머지 필요한 프로그램 및 ruby 자동 설치 완료 후 아래 명령 실행

        > source $HOME/.rvm/scripts/rvm

        ![](http://i.imgur.com/wWYsmQI.png)

        rvm 스크립트를 `bashrc`에 등록

        > echo "source $HOME/.rvm/scripts/rvm" >> ~/.bashrc


## Octopress 설정

1. `octopress repo`를 로컬에 clone 후 bundler로 관련 프로그램 설치

    다음의 명령 차례로 실행

    > git clone git://github.com/imathis/octopress.git octopress

    > cd octopress

    > gem install bundler

    > bundle install

    ![](http://i.imgur.com/VfqQohw.png)

    ![](http://i.imgur.com/QSmnYlp.png)

2. 기본 테마 기준으로 source 폴더에 초기 파일 생성

    > rake install

    ![](http://i.imgur.com/zXx7ykO.png)


## Github Respository 생성

GitHub 에서 이름이 GitHub_UserName.github.io 인 repository를 새로 생성한다(앞으로 `GitHub repo`라 한다).

나중에 이 `GitHub repo`에서 블로그 컨텐츠를 관리하게 된다.

![](http://i.imgur.com/ivZZLBM.png)


## Octopress - GitHub 연계

1. octopress에서 제공하는 GitHub 연계 자동 설정 프로그램 실행

    > rake setup_github_pages

2. `GitHub repo`의 url 입력

    ![](http://i.imgur.com/LXjTPk3.png)

`rake setup_github_pages`는 아래의 사항을 처리한다.

- imathis/octopress를 가리키고 있던 `origin`을 `octopress`로 이름 변경
- `origin`이 `GitHub repo`를 가리키도록 설정
- active 브랜치를 `master`에서 `source`로 변경(즉 `master` 브랜치는 없어지고 `source` 브랜치 생성)
- 블로그 URL 설정
- octopress에 의해 생성된 최종 블로그 내용을 담는 `_deploy` 폴더에 별도의 repo(앞으로 `deploy repo`라 한다)와 `master` 브랜치 생성

결론적으로 블로그를 생성하는 `octopress repo`는 `GitHub repo`의 `source` 브랜치로 저장되고,

octopress에 의해 생성되는 블로그 컨텐츠를 담고 있는 `deploy repo`의 `master` 브랜치가 `GitHub repo`의 `master` 브랜치로 저장되며,

`http://GitHub_UserName.github.io/`로 접근하면 `GitHub repo`의 `master` 브랜치의 내용(즉, `deploy repo`에서 push 된 내용)이 브라우저에 표시된다.

## 블로그 생성 및 미리 보기

1. 블로그 생성, markdown으로 작성한 포스트의 html 변환 등 수행

    > rake generate

    ![](http://i.imgur.com/BzDm3r9.png)

    화면에서 보는 것처럼 source 폴더에 있는 .markdown 파일을 _config.yml 파일에 설정된 내용에 따라 .html 파일로 변환해서 public 폴더에 저장한다.

2. 블로그 미리 보기

    `rake generate`으로 생성된 블로그를 아래의 명령으로 미리보기 할 수 있다.

    > rake preview

    ![](http://i.imgur.com/JN1ygQL.png)

    - 위와 같이 `write public/stylesheets/screen.css` 까지 화면에 찍히면 브라우저에서 `http://localhost:4000/`로 접속해서 미리 보기를 확인할 수 있다.

    ![](http://i.imgur.com/I2lvl3n.png)


## GitHub에 deploy

일단 미리보기가 제대로 나온다면 기본적으로 블로그를 만들 준비는 되었다.

이 상태로 먼저 GitHub에 올려서 준비 단계를 마치자.

GitHub에 올리는 방법은 두 가지가 있다.

1. Octopress가 제공하는 rake deploy 이용

    Octopress에서는 rake를 통해 GitHub에 쉽게 deploy하는 프로그램도 제공한다.

    > rake deploy

    ![](http://i.imgur.com/MZKs2uq.png)

    ![](http://i.imgur.com/zvQpPy7.png)

    GitHub의 계정 정보를 입력한다.

    ![](http://i.imgur.com/m6rdL7l.png)

    git pull 이 제대로 수행되지 않아 발생하는 오류인데, 화면에서 안내해 준대로 다음의 명령을 수행해서 remote 브랜치를 설정해준다.

    > cd _deploy

    > git branch &#45;&#45;set-upstream-to=origin/master master

    를 실행하고, 다시 `rake deploy` 실행

    ![](http://i.imgur.com/F64CUlx.png)

    Merge MSG 화면에서 CTRL+X 로 빠져나오면 다음과 같이 Push를 위해 GitHub 계정 정보를 묻는다.

    ![](http://i.imgur.com/WyyTiD4.png)

    계정 정보를 입력하면 Push가 완료된다.

    ![](http://i.imgur.com/3kF7CCW.png)

    이제 GitHub_UserName.github.io에 접근하면 다음과 같이 GitHub에 deploy된 기본 블로그를 확인할 수 있다.

    ![](http://i.imgur.com/QGODGpU.png)

2. 일반적인 Git commit/push 활용

    `rake deploy`도 사실 Git 명령을 wrapping한 것에 불과하다(자세한 내용은 `Rakefile` 파일을 열어보면 알 수 있다).

    따라서 당연히 직접 Git로도 가능한데, 게시물 작성 후 `rake generate`에 의해 .html로 변환된 내용이 들어있는 public 폴더의 내용을 _deploy 폴더로 복사한 후 git add/commit/push를 수행하면 된다. 이 방식으로 하면 커밋 메시지를 원하는 대로 작성할 수 있는 장점도 있다.

    > rake generate

    > cp -rf public/. _deploy

    > cd _deploy

    > git pull origin master

    > git add .

    > git commit -m '커밋 메시지'

    > git push origin master


----------

이걸로 Octopress로 GitHub에 블로그를 만들어 게시하는 것 까지는 성공했다.

기본 테마와 폰트 등 맘에 들지 않는 구석이 많지만 1탄은 여기까지로 하고,

2탄에서는 첫 번째 블로그 게시글(.markdown 파일)을 작성하고, 블로그로 게시할 수 있는 .html 파일로 변환하고, GitHub에 배포해보자.
