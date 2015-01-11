---
layout: post
title: "Octopress로 GitHub에 블로그 만들기-4"
date: 2015-01-11 00:46:00 +0900
comments: true
categories: [Octopress, GitHub, blog]
---

## 폰트 변경

개인 취향이겠지만 Octopress 에서 제공하는 기본 폰트는 한글이 그다지 예쁘게 보이지 않는다. 그래서 이번엔 웹 폰트를 써서 나눔 고딕으로 블로그의 폰트를 바꿔보자.

먼저 웹 폰트를 사용하기 위한 css 정보를 알아보고, 웹 폰트를 블로그에 적용하는 방법을 알아보자.

### 나눔 고딕 웹 폰트 CSS

http://www.google.com/fonts/earlyaccess 에서 korean으로 텍스트 검색을 하면 여러 가지 한글 웹 폰트를 볼 수 있다. 

나눔 고딕 폰트에 대한 CSS 정보는 다음과 같다.

> @import url(http://fonts.googleapis.com/earlyaccess/nanumgothic.css);

나눔 고딕 폰트를 적용할 문서 요소에 아래와 같이 `font-family`를 지정해주면 된다. 

> font-family: 'Nanum Gothic', serif;

### 블로그 적용 방법

블로그에 적용하려면 위 내용을 어느 CSS 파일에 적용해야 되는 지 알아야 한다.

결론적으로 `octopress repo/sass/custom/_style.scss` 에 아래의 내용을 추가하면 된다.

``` css
@import url(http://fonts.googleapis.com/earlyaccess/nanumgothic.css);
body, a, h2, h3, h4, code  {
	font-family: 'Nanum Gothic', serif;
}
```

`rake preview`를 실행 하면 폰트가 바뀐 것을 확인할 수 있다.

#### 폰트 변경 전

![](http://i.imgur.com/sanOiv5.png)

#### 폰트 변경 후

![](http://i.imgur.com/tvEgAwS.png)

### Octopress 의 CSS 생성 방식

결론적으로 `_style.css` 만 수정하면 쉽게 웹 폰트를 적용할 수 있었는데, 내친 김에 그 메커니즘도 살짝 알아보고 가자.

`rake generate`나 `rake preview`를 실행 했을 때의 화면을 주의 깊게 봤다면 `screen.css` 파일을 새로 생성하는 것을 알 수 있었을 것이다.

Octopress는 `octopress repo/sass/screen.scss` 파일을 이용해서 블로그에 실제 사용되는 최종적이고 유일한 CSS 파일인 `screen.css` 파일을 생성한다. `octopress repo/sass/screen.scss` 파일을 열어보면 다음과 같다.

``` css
@import "compass";
@include global-reset;

@import "custom/colors";
@import "custom/fonts";
@import "custom/layout";
@import "base";
@import "partials";
@import "plugins/**/*";
@import "custom/styles";
``` 
즉, `octopress repo/sass/custom/_styles.scss` 에 의해 생성되는 `custom/styles` 파일을 가장 나중에 import 하므로, 다른 CSS에 설정된 내용보다 `_styles.scss`에 설정된 내용이 우선 적용되기 때문에 결론적으로 `_style.scss`에 웹 폰트 관련 내용을 적용하면 되는 것이다.

실제로 `octopress repo/sass/custom/_styles.scss` 파일을 열어보면 주석에 관련 내용이 설명되어 있다.

``` css
// This File is imported last, and will override other styles in the cascade
// Add styles here to make changes without digging in too much
@import url(http://fonts.googleapis.com/earlyaccess/nanumgothic.css);
body, a, h2, h3, h4, code  {
	font-family: 'Nanum Gothic', serif;
}
```

최종 생성되는 `octopress repo/public/stylesheets/screen.css` 파일을 열어보면(모든 내용이 한 행으로 작성되어 있어 보기 편하지는 않다) 맨 마지막 부분에 `_styles.scss`에서 지정한 내용이 추가되어 있는 것을 확인할 수 있다.

![](http://i.imgur.com/emCEHMV.png)
 
