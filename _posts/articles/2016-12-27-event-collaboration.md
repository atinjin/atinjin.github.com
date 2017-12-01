---
layout: post
title: Event Collaboration
categories: articles
excerpt:
tags: [system, event]
image:
  feature:
comments: true
share: true
modified: 2016-12-26T17:40:26+09:00
---

# Event Collaboration

## 기존 시스템에서의 협업 방법

현재 시스템에서는 기본적으로 “Request”를 이용하여 자료를 처리하는 것으로 가정하고 있다.  이는 Responsibility를 명확히 할 수 있고, 데이터 처리의 시작과 끝( Transaction)을 관리할 수 있다는 장점이 있다. 단점이라고 한다면 모든 것이 관리 영역내에 있어야 한다는 것이다. “Requester”는 어떤 명령(Command)를 어떤 Component에 보내서 어떤 Response를 받을지 알아야 한다는 것이다. 

![Command를 이용한 협업]({{ site.url }}/images/command_based_service.png)

그러나 새로운 방식이 있다. 이는 “Event”를 적극적으로 활용한 것이다.

![Event를 이용한 협업]({{ site.url }}/images/event_based_service.png)

이와 같은 구조가 갖는 가장 큰 장점은 서비스간 의존성이 사라진다는 것이다.
