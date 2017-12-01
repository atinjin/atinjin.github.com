---
layout: post
title: Don't Reinvent the Wheel
modified:
categories: blog
excerpt:
tags: [data_structure, algorithm]
image:
  feature:
comments: true
share: true
modified: 2016-08-19T08:11:09+09:00
---

# 바퀴를 또 발명하려 하지 마세요.

![reinvent the wheel](http://www.scotthoward.me/wp-content/uploads/2016/02/q.png)

최근에 있었던 일입니다. 문제 상황은 다음과 같았습니다.

## Practical Problem
DB에 데이터가 저장되어 있다. 저장되는 데이터에는 순번을 부여한다. 데이터의 수에는 제한이 없다.(실제 제한은 저장 공간 제한밖에 없다.) 이런 상황에서 데이터의 순번이 중간에서 추가/삭제하는 경우 DB 트랜잭션 시간을 최소화할 수 있는 방법이 있을까?

DB의 특정 테이블의 row마다 순번이 메겨져 있을 경우, 순번을 미루거나 당기기 위해 변경되는 row 뒤에 있는 "모든 row에 대해서 **update** 쿼리를 해야 하나?"라는 문제였다. 어떤 해결 방법이 있을까? 나는 다음과 같은 문제 해결 과정을 생각해보았다.


## Problem Abstraction
다음과 같이 실제 문제를 [추상화](https://ko.wikipedia.org/wiki/%EC%B6%94%EC%83%81%ED%99%94_(%EC%BB%B4%ED%93%A8%ED%84%B0_%EA%B3%BC%ED%95%99)) 해보았다.

모든 아이템에 순서를 부여해야한다. 아이템의 수는 선형적으로 늘어날 수 있고 수의 제한이 없을 수도 있다. 이 때 **아이템의 순서 변경**시 계산을 최소화할 수 있는 방법은 무엇일까?

추상화된 문제는 어디선가 많이 보던 문제이다. 바로 "배열(Array)"에 대한 문제와 같았다. 배열을 정렬할 때 중간에 어떤 원소를 집어 넣어야 할 경우 보통은 하나씩 옆칸으로 복사한 후 공간을 만들어 추가를 한다. 그러나 이러한 경우 **원소 추가**마다 O(n)의 수행 시간이 걸리기 때문에 문제가 될 수 있다. 그래서 생각해낸것이 **Linked List**이다.

![Linked List](http://people.engr.ncsu.edu/efg/210/s99/Notes/LLdefs.gif)


> The principal benefit of a linked list over a conventional array is that the list elements can easily be inserted or removed without reallocation or reorganization of the entire structure because the data items need not be stored contiguously in memory or on disk, while an array has to be declared in the source code, before compiling and running the program. Linked lists allow insertion and removal of nodes at any point in the list, and can do so with a constant number of operations if the link previous to the link being added or removed is maintained during list traversal.
[wiki](https://en.wikipedia.org/wiki/Linked_list)

이 상황에 정확히 맞는 자료 구조(Data Structure)이다.

여기서 Linked List 컨셉을 적용하기로 했을 때 생길 수 있는 문제점도 생각해보아야 한다.

> On the other hand, simple linked lists by themselves do not allow random access to the data, or any form of efficient indexing. Thus, many basic operations — such as obtaining the last node of the list (assuming that the last node is not maintained as separate node reference in the list structure), or finding a node that contains a given datum, or locating the place where a new node should be inserted — may require sequential scanning of most or all of the list elements.[wiki](https://en.wikipedia.org/wiki/Linked_list)

단점은 바로 검색이다. 배열과 같이 인덱스를 이용하여 **array[12]** 접근할 수 없기 때문이다. 그러나 이러한 특성은 해당 아이템을 인덱스를 이용하여 접근하지 않기 때문에 문제가 되지 않았다.

여기서 "Linked List"의 장단점을 정리하면 다음과 같다.

## Advantages
- Linked lists are a dynamic data structure, which can grow and be pruned, allocating and deallocating memory while the program is running.
- Insertion and deletion node operations are easily implemented in a linked list.
- Linear data structures such as stacks and queues are easily executed with a linked list.
- They can reduce access time and may expand in real time without memory overhead.

## Disadvantages
- They use more memory than arrays because of the storage used by their pointers.
- Nodes in a linked list must be read in order from the beginning as linked lists are inherently sequential access.
- Nodes are stored incontiguously, greatly increasing the time required to access individual elements within the list, especially with a CPU cache.
- Difficulties arise in linked lists when it comes to reverse traversing. For instance, singly linked lists are cumbersome to navigate backwards[1] and while doubly linked lists are somewhat easier to read, memory is wasted in allocating space for a back-pointer.


## Reinventin the wheel 

[Reinventing the wheel](https://en.wikipedia.org/wiki/Reinventing_the_wheel) 이란 말이 있습니다. 인류의 역사가 흐르면서 기술(Technology)은 물론 지식(Knowledge) 역시 축적되었습니다. 그래서 우리가 생각하는 또는 부딪히는 대부분의 문제는 과거에 누군가가 한번쯤은 고민해보았던 문제가 대부분입니다. 내가 생각했던 문제를 100년 전의 나보다 더 훌륭한 사람 또는 사람들이 고민해보고 해결책을 찾아보았다면 어느 정도 수용 가능한 답을 내놓았을 것입니다. 그럴 경우 내가 다시 한번 고민해보는 것 보다 이를 받아들이고 빠르게 더 중요한 문제로 나아가는 것이 좀 더 생산적일 수 있습니다.

인류의 지식은 축적되어 나가야 합니다. 축적된 기술이 기술의 진보를 만들어내고 그러한 진보가 인간의 행복 증진에 쓰일 수 있기 때문입니다. 이를 위해서는 꾸준한 공부가 뒷받침되어야 합니다.
