---
layout: post
title: Traveling Sales-man Problem
categories: blog
excerpt:
tags: [algorithm, TSP, programming]
image:
  feature:
comments: true
share: true
modified: 2016-08-09T08:32:11+09:00
---

# Traveling Sales-man Problem

<figure>
    <a href="https://static01.nyt.com/images/2012/03/14/theater/14salesman-map/14salesman-map-custom1.jpg"><img src="https://static01.nyt.com/images/2012/03/14/theater/14salesman-map/14salesman-map-custom1.jpg"></a><br>
    <caption>외판원 여행 문제</caption>
</figure>


## 문제
택배 배달원이 있습니다. 새벽부터 집하장에 가서 오늘 배달해야 할 택배 물품을 받아왔습니다. 그리고 배달해야 할 택배들의 주소를 훓어 보았습니다. 가야할 위치를 크게 나누어보니 10군데 정도였습니다. 그리고 어디부터 가야 가장 빠르게 배달할 수 있을지 고민해봅니다. 직관적으로 가장 가까운 곳을 찾아가는 방법(Greedy Algorithm)을 사용하는 것도 좋지만 IT 시대에 컴퓨터를 이용하여 최적의 경로(Path)를 찾아보고 싶습니다.

## Exhaustive Search 이용
크게 이동해야 할 위치가 제한적(10곳)이기 때문에 Exhaustive Search(완전 탐색)을 통해 충분히 최적의 배달 경로를 찾을 수 있습니다. 최대 10!(=3,628,800)개의 경우의 수만 확인해보면 됩니다. 그럼 이를 해결할 수 있는 코드를 짜보아야겠습니다.
 
## D&C 이용
경로를 선택하면 나머지 남은 곳에서 최적의 경로를 찾으면 됩니다. 즉, 문제를 계속해서 작은 문제로 나누어 갈 수 있는 문제입니다. 이러한 경우 적용할 수 있는 문제 해결 알고리즘은  바로  **Divide & Conquer** 방식입니다. 또한 D&C 방식을 쉽게 구현할 수 있는 Pattern은 *Recursive Function*을 구현하는 것입니다.
![divide and conquer](http://bigdata.ices.utexas.edu/wp-content/uploads/2014/03/divide-and-conquer1.png)

## 해결 시나리오
- 초기값
  - 시작 장소를 결정한다.(어떤 곳을 선택하든 상관없다. 왜냐하면 되돌아 올 것이기 때문이다.)
- Recursive Function
  - Base case를 설정한다.	
  - 시작 위치를 제외한 나머지 위치를 이용하여 최단 거리를 구한다.
  - 최단 거리인지 확인한다.

## Pseudo Code
~~~java
boolean[] location; //배달해야 할 장소 리스트(본 문제에서는 10군데이다.)
int[][] distance; //distance[a][b]는 a와 b 사이의 거리를 의미한다.
Stack<Integer> paths; //지나간 경로를 저장한다.
long findMinPath(long totalDistance, Stack<Integer> paths, boolean[] location) {
	//Base case
	if(paths.size() == location.length) {
		//10군데를 모두 돌아보았다.
		//다시 시작 위치로 돌아가는 거리를 더하면 이번 케이스의 최종 거리가 나온다.
		return totalDistance + distance[0][paths.peek()] 
	}
		
	//calculate the minimum distance
	long result = Long.MAX_VALUE;
	//모든 경우의 수를 다 세보자.
	for(int next=0; next<location.length; next++) {
		//이미 방문한 곳은 지나가자. 
		if(location[next] != true) { 
			location[next] = true; //방문록 남기고
			paths.push(next); //경로에 표시해주고
			//자, 이제 최소값을 구하기 위해 Recursive Call을 사용할 시기이다.
			totalDistance += distance[paths.peek()][next]
			long recursiveResult = findMinPath(totalDistance, paths, location)
			result = (recursiveResult < result)?recursiveResult:result;
			//여기까지 왔다는 것은 10군데 모두를 들렀다는 것이다.
			//이번 시도를 Revert하고 다음 장소부터  또 다시 시도해본다.
			paths.pop();
			location[next] = false;
		}		
	}
	return result;
}
~~~ 
 
## Recursive Call을 했다는 것의 의미??
Recursive Function을 실행했다는 것은 심각한 문제입니다. **무한 루프**에 빠지는 것이기 때문입니다. Recursive Call은 같은 함수 안에서 같은 함수를 불렀다는 이야기이고, 그 함수는 또 다시 자신을 부를 것이고 이는 끝없이 불리다가 아무 성과없이 *StackOverFlow*로 끝날 것입니다. 비참하게 말이죠.
그래서 Recursive Function에는 안전 장치가 필요합니다. 그것이 바로 **Base Case** 입니다. 바로 Recursive Call의 탈출구입니다. 끝없을 것 같았던 무한 루프를 탈출시키는 워프 역할을 합니다.
<figure>
    <a href="http://www.popsci.com/sites/popsci.com/files/styles/large_1x_/public/import/2013/images/2013/03/thwarpdrive_980.jpg?itok=eu3bZABd"><img src="http://www.popsci.com/sites/popsci.com/files/styles/large_1x_/public/import/2013/images/2013/03/thwarpdrive_980.jpg?itok=eu3bZABd"></a>
    <caption>무한 루프의 탈출구</caption>
</figure>

## 10군데 이상이면 어떻하죠?
10군데 이상이면 문제입니다. [12!](https://en.wikipedia.org/wiki/Factorial) 만 되더라도 총 경우의 수는 479,001,600개 입니다. 보통 CPU가 2GHz라고 했을때, 초당 2억번의 계산을 할 수 있다고 할 수 있습니다. 그러면 12!의 경우는 2초 이상이 걸리기 때문에 1초라는 제한 시간내에 풀어낼 수가 없습니다. 어떻게 해야 할까요?

![멘붕](https://cdn.namuwikiusercontent.com/87/872f372fcd5460278c71a34e02b80656bb4198d591ceb72c17bdeb262c6d8290.png?e=1476752784&k=tySt3YPlntI3f_z_-mxoeg "최적화 방법을 찾아야 해!")

뭐~~~ 다른 방법을 찾아야죠...
