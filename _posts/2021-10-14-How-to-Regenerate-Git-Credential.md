---
layout: post
title: How to Regenerate Git Credential
description: How to Regenerate Git Credential
summary: How to Regenerate Git Credential
tags: [git]
---

# via Command line
- 심플하게 아래의 커맨드를 터미널을 이용해 입력하면, 나의 컴퓨터에 등록된 credential 키체인 정보를 초기화할 수 있다.
`git credential-osxkeychain erase`
- 이후에 `git push` 를 진행하면, credential 을 새롭게 입력하라고 안내가 나온다. 