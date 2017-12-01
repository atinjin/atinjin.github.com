---
layout: post
title: Octopress를 이용한 Blog Posting
categories: blog
excerpt: 지킬에서 쉽게 포스트 쓰기
tags: [octopress, posting]
comments: true
share: true
image:
  feature:
date: 2017-12-01T13:46:51+09:00
modified:
---

# Octopress 란?

![Octopress Image](\images\octopress-image.jpg)

_Octopress_ 는 지킬 블로그에 포스트를 쉽게 쓸 수 있도록 도와주는 도구입니다.

다음과 같은 명령어를 사용하여 다양한 블로깅 작업을 손쉽게 해결해줍니다.

```
init <PATH>         # Adds Octopress scaffolding to your site
new <PATH>          # Like `jekyll new` + `octopress init`
new post <TITLE>    # Add a new post to your site
new page <PATH>     # Add a new page to your site
new draft <TITLE>   # Add a new draft post to your site
publish <POST>      # Publish a draft from _drafts to _posts
unpublish <POST>    # Search for a post and convert it into a draft
isolate [POST]      # Stash all posts but the one you're working on for a faster build
integrate           # Restores all posts, doing the opposite of the isolate command
deploy              # deploy your site via S3, Rsync, or to GitHub pages.
```

이때 참조되는 템플릿 파일은 다음과 같이 설정 파일에서 정할 수 있습니다.

```
# Default extension for new posts and pages
post_ext: markdown
page_ext: html

# Default templates for posts and pages
# Found in _templates/
post_layout: post
page_layout: page

# Format titles with titlecase?
titlecase: true

# Change default template file (in _templates/)
post_template: post
page_template: page
draft_template: draft
```

CLI 형식은 다음과 같습니다.

```
$> octopress new draft "제목"
$> octopress publish "제목"
```
