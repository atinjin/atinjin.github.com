---
layout: post
title: What Is the Erlang?
categories: blog
excerpt: What Is the Erlang?
tags: [language, erlang, functional, programming]
comments: true
share: true
image:
  feature: so-simple-sample-image-5.jpg
header-img: Erlang_logo.png
subtitle: "최근 다양한 프로그래밍 언어가 나오고 있습니다.
얼랭의 경우 개발된지 오래된 언어지만 그 특장점 때문에 현재도 쓰이고 있는 언어입니다.
언어에 맞는 솔루션 분야가 있습니다."
author: Ryan Jin
date: 2017-12-01T14:30:43+09:00
modified:
---

# Erlang 프래그래밍 랭귀지

언어마다 특징을 가지고 있습니다. 그 특징은 언어의 탄생 배경과 연관이 있습니다. 지금부티 보게될 얼랭이라는 프로그래밍 언어는 다음의 두가지 키워드로 정의할 수 있습니다.

- 안정성
- 동시성

각각의 목적을 달성하기 위해서 어떠한 장치를 준비했는지 알아보겠습니다.
얼랭은 덴마크 수학자 이름이자 "Ericsson Language"의 약자이기도 합니다. 얼랭은 CouchDB, Amazon SimpleDB, Facebook 채탱 프로그램에도 쓰입니다. 

<figure class="half">
	<img src="https://upload.wikimedia.org/wikipedia/en/thumb/f/f8/CouchDB.svg/256px-CouchDB.svg.png">
	<img src="https://upload.wikimedia.org/wikipedia/uk/4/40/Simpledb.jpg">
	<figcaption>Apache CouchDB / Amazon SimpleDB<figcaption>
</figure>

# 안정성을 위해 Let it be. 

> 안전한 프로그램이란 무엇일까요?

"절대로 죽지않는 것이다."라고 정의할 수 있습니다. 어떠한 입력값이 들어온다고 해도 모두 처리할 수 있고, 간혹 처리할 수 없을 경우에는 예외 처리가 되어 사용자 또는 개발자가 인지할 수 있는 상태일 경우를 말합니다.

그래서 좋은 프로그래머는 모든 상황에 대한 처리가 가능하도록 if문, switch문을 작성합니다. 한마디로 좋은 코드라고 할 수 있습니다.

그러나 세상의 모든 케이스를 커버하긴 힘들 것입니다. 특히나 복잡하고 지속적으로 확장해 나가는 소프트웨어의 경우는 논리적인 원인 외에도 다양한 외부 원인으로 프로그램이 죽는 경우가 생깁니다 이런 경우에 대해서는 다른 방향으로 안정성을 추구해야 합니다.

> Let it crash.

얼랭에서는 프로세스를 가볍게 만들어서 만들고 없애는 작업을 쉽게 하였습니다. 여기에 모니터링 기능을 더해 프로세스가 죽더라도 이를 빨리 인지하고 다시 프로세스를 살리는 등의 조치가 가능하게 했습니다.

> 무중단 코드 변경(Code hot-swap)

# 동시성

> 쓰레드는 없다. 프로세스만 있을뿐

동시성 제약이 가장 많은 부분은 리소스 공유에 따른 Lock입니다. 이를 위해서 얼래의 경우 쓰레드를 사용하지 않고 프로세스만을 사용합니다. 프로세스의 경우 고유의 리소스를 가지고 있기 때문에 리소스 Lock이 불필요하게 됩니다.

# Almost Fuctional Langauge

함수형 언어로서 다음과 같은 특징을 가집니다. 완전한 함수형 언어인 Haskel과 달리 약간의 예외 상황이 존재합니다. 그래서 _Almost_ 입니다.

- 함수만 있다.(객체는 없다)
- Almost 함수는 동일한 입력에 동일한 출력을 낸다.
- Almost No side-effect
- 변수에 값을 딱 한번만 할 수 있다.

----






