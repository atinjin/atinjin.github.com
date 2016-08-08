---
layout: post
title: Traveling Sales-man Problem
modified:
categories: blog
excerpt:
tags: [algorithm, TSP]
image:
  feature:
date: 2016-08-09T08:32:11+09:00
---

# Traveling Sales-man Problem

## 문제
택배 배달원이 있습니다. 새벽부터 집하장에 가서 오늘 배달해야 할 택배 물품을 받아왔습니다. 그리고 배달해야 할 택배들의 주소를 훓어 보았습니다. 가야할 위치를 크게 나누어보니 10군데 정도였습니다. 그리고 어디부터 가야 가장 빠르게 배달할 수 있을지 고민해봅니다. 직관적으로 가장 가까운 곳을 찾아가는 방법(Greedy Algorithm)을 사용하는 것도 좋지만 IT 시대에 컴퓨터를 이용하여 최적의 경로(Path)를 찾아보고 싶습니다.

## Exhaustive Search 이용
크게 이동해야 할 위치가 제한적(10곳)이기 때문에 Exhaustive Search(완전 탐색)을 통해 충분히 최적의 배달 경로를 찾을 수 있습니다. 최대 10!(=3,628,800)개의 경우의 수만 확인해보면 됩니다. 그럼 이를 해결할 수 있는 코드를 짜보아야겠습니다.
 
## D&C 이용
경로를 선택하면 나머지 남은 곳에서 최적의 경로를 찾으면 됩니다. 즉, 문제를 계속해서 작은 문제로 나누어 갈 수 있는 문제입니다. 이러한 경우 적용할 수 있는 문제 해결 알고리즘은  바로  Divide & Conquer 방식입니다. 또한 D&C 방식을 쉽게 구현할 수 있는 Pattern은 Recursive Function을 구현하는 것입니다.

## 해결 시나리오
- 초기값
  - 시작 장소를 결정한다.(어떤 곳을 선택하든 상관없다. 왜냐하면 되돌아 올 것이기 때문이다.)
- Recursive Function
  - 시작 위치를 제외한 나머지 위치를 이용하여 최단 거리를 구한다.
  - 최단 거리

## Pseudo Code
 
 