---
layout: post
title: Dynamic Programming
modified:
categories: blog
excerpt:
tags: []
image:
   feature:
date: 2016-08-04T16:41:36+09:00
---

<figure>
	<a href="{{ site.url }}//images/knapsack.svg"><img src="{{ site.url }}//images/knapsack.svg"></a>
	<caption></caption>
</figure>

## 개념
번역하면 동적 계획법이라고 할 수 있습니다. 하나의 문제를 풀기 위해서 큰 단위의 문제를 작은 단위의 문제로 나누는 **Devide and Conquar** 방식을 사용합니다. 여기에 더하여 **중복**되는 계산 결과를 저장(*Memoization*)하는 과정을 추가합니다. 이를 이용하여 전체 계산 과정 중 중복되는 결과값을 캐쉬(*cache*)에 저장 해두었다가 재활용하여 계산 속도를 향상시키는 기법입니다.

## 구현 패턴
- Exhaustive Search 패턴 + Memoization 패턴

## Memoization 구현 패턴
- cache 초기화
- 계산 이전에 cache에서 결과값 유무 확인
- 계산된 결과값이 있을 경우 바로 사용, 없을 경우 계산하여 cache에 저장

## 예시
### 문제
N x N 크기의 게임판에 1~9까지의 정수가 각 칸에 적혀 있다고 하자. 이 때, (0,0)에서 시작하여 각 칸에 쓰여진 숫자만큼 오른쪽 또는 아래쪽으로 이동할 수 있다. (n, n)에 도달할 수 있는지 여부를 판단하세요.

### 풀이 1) Exhaustive Search로 풀기
~~~
boolean isReachable(int[][] board, int x, int y) {
 	int n = board.length;
	//Boundary Condition
	if(x >= n || y >= n)
		return false;
		
	//Base Case
	if(x == n-1 && y == n-1)
		return true;
		
	//Calculate
	return isReachable(board, x+board[x][y], y)
			|| isReachable(board, x, y+board[x][y]);
}
~~~
풀이 1번은 Recursive Function을 사용(**Recursion**)하여 Exhausive Search로 문제를 풀었습니다. 여기서 주의할 점은 경계 조건(*Boundary Condition*)과 **Off-by-one error**입니다. 두가지 모두 익숙하지 않으면 놓칠 수 있는 부분이니 항상 확인하는 습관이 필요합니다.

### 풀이 2) Dynamic Programming으로 변환
~~~
int[][] cache;
void init(int[][] cache) {
	for(int i=0; i<n; i++)
		for(int j=0; j<n; j++)
			cache[i][j] = -1;
}
boolean isReachable(int[][] board, int x, int y) {
 	int n = board.length;
	//Boundary Condition
	if(x >= n || y >= n)
		return false;
		
	//Base Case
	if(x == n-1 && y == n-1)
		return true;
	
	//Use cache
	if(cache[x][y] != -1)
		return cache[x][y];
	else {
		//Calculate
		boolean result = isReachable(board, x+board[x][y], y)
				|| isReachable(board, x, y+board[x][y]);
		cache[x][y] = result;
		return result;
	}
}
~~~
풀이 2번의 경우는 풀이 1번에 Memoization 기법을 추가한 형태입니다. 여기서 어떤 요소들이 고려되어 추가되었는지  익힐 필요가 있습니다.

첫번째는 **cache 생성**입니다. 계산 결과값을 저장하기 위한 구조입니다. 그런데 단순히 *된다* 또는 *안된다*는 boolean값을 데이터형으로 가지지 않습니다. 그 이유은 cache의 경우 계산값을 가지는지 가지지 않는지 상태값이 추가되어야 하기 때문입니다. 그래서 이 문제의 경우는 3가지 값

- *계산전* = -1
- *가능* = 1
- *불가능* = 0

을 표시하기 위해서 Integer형을 사용하였습니다.

두번째는 **cache를 사용**하는 것입니다. 값을 계산(*Calculate*)하기 전에 cache를 확인하고 값의 유무에 따라 계산 과정을 지나치게(*skip*)하는 것이 Dynamic Programming의 핵심이기 때문입니다.

## 마무리
지금까지 Exhausive Search 알고리즘의 성능을 향상시키는 방법인 Dynamic Programming에 대해서 알아보았습니다. 프로그래밍에서 성능 향상을 위해서 자주 사용하는 부분이 캐쉬입니다. 웹서비스도 그렇고 데이터 베이스도 마찬가지로 캐쉬를 사용하여 전체적인 성능을 향상시킬 수 있습니다. 불필요한 중복을 없애는 Dynamic Programming을 실제 코딩에도 적용하여 프로그램의 반응 속도를 향상 시켜볼 수 있습니다. 이를 위해서 선행되어야 할 과정은 로직 중에서 반복되어 로딩하거나, 계산하는 부분이 있는지를 찾아보는 것입니다. 반복되는 빈도가 높을수록 유용한 알고리즘이기 때문에 적절한 곳에 사용할 수 있도록 평소에도 연습하는 것이 필요합니다.


