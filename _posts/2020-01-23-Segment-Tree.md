---
layout: post
title : "세그먼트 트리 (Segment Tree, 구간 트리)"
excerpt : "세그먼트 트리를 알아보자!"
date : 2020-01-23-16:19
tags : [Segment Tree, Fenwick Tree, Lazy-propagation]
category : [Algorithm]
comments : true
author: Kimcoding
feature: https://i.imgur.com/R0aqtbF.png
catalog : true
---

<br/>
## 세그먼트 트리란?
<br/>

배열 전체 구간 1~n 중에 a~b 구간의 쿼리를 구하거나 배열 인덱스 a의 값을 바꿀 때 O(lgN)의 시간 복잡도를 가지는 자료구조입니다.

---
<br/>

## 그거 왜 배워요??
<br/>

배열 arr[1000001]의 1~1000000  구간 합 쿼리를 구해서 출력해봅시다.

연속합을 이용하면 1~1000000을 O(1) 만에 구할 수 있지만 arr[2020]의 값을 변경한다고 했을 때

배열 2020 인덱스 이후로 연속합이 변경이 되어야 하기 때문에 상수 시간 안에 구할 수가 없습니다.

반복문을 이용하여 arr[1] + arr[2] + ··· + arr[1000000]을 더한 값을 출력합니다.  (query, O(N))

arr[2020]의 값을 x로 변경합니다. (update, O(1))

다시 반복문을 이용하여 arr[1] + arr[2] + ··· + arr[1000000]을 더한 값을 출력합니다. (query, O(N))

<br/>

이 연산을 M 번 반복한다고 하면 M * O(update + query) = M * O(1 + N) = M * O(N) = O(MN)입니다.

N은 1000000으로 정했으니 M이 100 정도만 돼도 1억이 됩니다.

<br/>

시간 복잡도를 줄이기 위해 세그먼트 트리를 사용하면

세그먼트 트리를 이용하여 arr[1] + arr[2] + ··· + arr[1000000]을 더한 값을 출력합니다.  (query, O(lgN))

arr[2020]의 값을 x로 변경합니다. (update, O(lgN))

다시 세그먼트 트리를 이용하여 arr[1] + arr[2] + ··· + arr[1000000]을 더한 값을 출력합니다. (query, O(lgN))

<br/>

이 연산을 M 번 반복한다고 하면 M * O(update + query) = M * O(lgN + lgN) = M * O(lgN) = O(MlgN)입니다.

<br/>

이런 유형의 시간을 줄여야 하는 문제들을 풀기 위해 세그먼트 트리를 배워야 합니다!

---
<br/>

## 세그먼트 트리 구현
<br/>

**구성**

배열, init 함수, update 함수, query 함수
<br/><br/>

**구현 방법**

top-down  확장성(lazy propagation), 직관적

bottom-up 구현 간단, 성능 좋음

<br/>

![](https://i.imgur.com/R0aqtbF.png)

<br/>

각 트리 노드마다 구간을 정해놓고 그 값을 저장할 것입니다. ex) 1 - 3 (1~3 구간 쿼리 저장)

<br/>

세그먼트 트리를 꽉 채우면 완전 이진 트리가 되므로

<br/>

**배열 크기 : 2^k 중에 n과 가까운 큰 값 \* 2**

ex) 12 -> 16 * 2 = 32, 7 -> 8 * 2 = 16, 4 -> 4 * 2 = 8 …

k = ceil(log2(n)) + 1으로 구합니다. (ceil - 올림 함수)

<br/>

트리 노드의 배열 인덱스는

**루트 노드 : 1**

**왼쪽 자식 노드 : 현재 노드 \* 2**

**오른쪽 자식 노드 : 현재 노드 \* 2 + 1**로 사용하겠습니다.

<br/>

![](https://i.imgur.com/iEgDeLV.png)

<br/>

---

<br/>

## TOP-DOWN

<br/>

이제 구간 합을 구하는 세그먼트 트리를 만들어 보겠습니다.



```cpp
// 세그먼트 트리 구조체 구조
struct SegmentTree {
	int* tree;
    int tree_size;
	SegmentTree(){}
	int init(){}
	void update() {}
	int query(){}
    ~SegmentTree(){}
};
```

<br/>

먼저 구조체를 생성할 때 트리 크기를 동적할당해주겠습니다.



```cpp
// 생성자 수정
SegmentTree(int n) {
	tree_size = 1 << ((int)ceil(log2(n)) + 1); // tree_size = n * 4;
	tree = new int[tree_size]();
}
```

<br/>

tree_size를 구하기 귀찮으면 n * 4를 할당하여 넉넉히 해도 됩니다. (물론 메모리는 낭비...)



이제 입력받은 배열 arr을 세그먼트 트리에 저장해보겠습니다.



```cpp
// arr - 입력받은 배열, now - 현재 노드 인덱스
// start - 현재 구간 시작 인덱스(x~y -> x), end - 현재 구간 끝 인덱스 (x~y -> y)
int init(int* arr, int now, int start, int end) {
	if (start == end)                 // 리프 노드 일때
		return tree[now] = arr[start];
	int mid = (start + end) / 2;
	return tree[now] = init(arr, now * 2, start, mid) + init(arr, now * 2 + 1, mid + 1, end);
}
```



![top-down init 함수 동작](https://i.imgur.com/1BogBkj.png)

<br/>

이런 식으로 재귀가 동작이 됩니다.

현재 범위가 1~6이라면 반을 나눠서 1~3과 4~6으로 각각 구간의 합을 구하도록 하면 됩니다.

그리고 1~3, 4~6의 구간의 합이 구해졌다면 그 두 값을 더한 값이 현재 구간의 합이 됩니다.

start == end은 위 그림처럼 리프 노드일 때 더 이상 자식이 없으니 arr의 값을 저장해주고 그 값을 반환해줍니다.

리프 노드가 아닐 경우 두 자식 노드의 값을 더한 값이 현재 구간의 합이 되므로 저장해줍니다.

저는 문제 풀 때 init 함수를 잘 구현하지 않습니다...

update 함수로 대체할 수도 있고 제가 푼 문제들은 진행하면서 하나씩 update를 하는 방식이었어서 쓸 일이 없었습니다... Pass!

<br/>

update 함수를 만들어보겠습니다.



```cpp
void update(int now, int start, int end, int idx, int val) { // idx - 값을 변경할 인덱스, val - 변경할 값
	if (start > idx || idx > end) return;  // 현재 구간에 idx가 포함되지 않았을 때
	if (start == end) tree[now] = val;     // 리프 노드
	else {
		int mid = (start + end) / 2;
		update(now * 2, start, mid, idx, val);
		update(now * 2 + 1, mid + 1, end, idx, val);
		tree[now] = tree[now * 2] + tree[now * 2 + 1];
	}
}
```

<br/>

init 함수와 크게 다르지 않습니다.

start == end 처리도 리프 노드일 때 값을 변경하는 것으로 똑같습니다.

리프 노드가 아닐 때도 init 함수와 동일하게 구간을 반으로 나눠서 update를 하고 바뀐 두 값의 합을 현재 인덱스에 저장합니다.

다른 점이 있다면 2번째 줄에 처리를 해준 부분이 있는데 arr[7] = {0,1,6,2,7,3,2}에서 arr[2]을 5로 바꾸는 예제를 그림으로 먼저 보겠습니다.

저는 0번째 인덱스를 잘 쓰지 않아 arr[1] ~ arr[6]까지 사용하겠습니다.

<br/>

![top-down update 함수 동작](https://i.imgur.com/tRFYxV6.png)

<br/>

arr[2]를 5로 바꿔봤습니다.

**위 그림처럼 2가 포함된 구간만 값을 변경해야 되므로 start <= idx <= end 가 아닌 idx 값을 보게 되면**

**구간의 값이 변동되지 않도록 바로 처리를 해줍니다.**

위와 같이 2가 포함되지 않은 구간의 값에는 영향을 주지 않습니다.

<br/>

query 함수를 만들어 보겠습니다.

<br/>

```cpp
// left - 구하고자 하는 구간의 시작 값, right - 구하고자 하는 구간의 끝 값
int query(int now, int start, int end, int left, int right) {
	if (end < left || right < start) return 0;                // 구하려는 구간이 현재 구간과 겹치는 부분이 없을 때
 	if (left <= start && end <= right) return tree[now];      // 현재 구간이 구하려는 구간 안에 포함되어 있을 때
	int mid = (start + end) / 2;
	return query(now * 2, start, mid, left, right) + query(now * 2 + 1, mid + 1, end, left, right);
}
```

<br/>

init, update 함수와 비슷합니다.

O(lgN)의 시간 복잡도를 위해 볼 필요가 없는 구간 혹은 한 번에 처리가 가능한 구간에서 바로 반환해줘야 합니다.

그래서 두 가지의 처리를 하였습니다.

<br/>

**첫 번째 처리는 구하려는 구간이 현재 보고 있는 구간과 겹치지 않을 때 더 이상 자식 노드들로 갈 필요가 없기 때문에**

**합에 영향을 주지 않는 0을 반환해줍니다. (left, right) < (start, end) || (start, end) < (left, right)**

<br/>

**두 번째 처리는 현재 보고 있는 구간이 구하려는 구간 안에 포함될 때 그 구간의 값이 필요하기 때문에**

**바로 그 구간의 합을 반환해줍니다. left <= (start, end) <= right**

<br/>

(2~5) 구간의 합을 구해보겠습니다.

<br/>

![top-down 쿼리 함수 동작](https://i.imgur.com/VRn7RaX.png)

<br/>

(1, 6) 구간부터 query 함수가 진행될 텐데 먼저 왼쪽 자식 노드를 봅니다.

(1,3) 구간에서 구하려는 (2,5) 구간과 겹치는 부분이 있기 때문에 왼쪽 자식 노드를 봅니다.

(1,2) 구간에서 구하려는 (2,5) 구간과 겹치는 부분이 있기 때문에 왼쪽 자식 노드를 봅니다.

(1,1) 구간에서는 (2,5) 구간과 겹치는 부분이 없어 0을 반환합니다.

(1,2)의 오른쪽 자식 노드인 (2,2) 구간이 (2,5) 구간 안에 포함되어 있기 때문에 현재 구간의 값을 반환합니다. (5)

(1, 2) 구간에서 왼쪽 구간의 값 + 오른쪽 구간의 값을 반환합니다. (0 + 5)

(1,3)의 오른쪽 자식 노드인 (3,3) 구간이 (2,5) 구간 안에 포함되어 있기 때문에 현재 구간의 값을 반환합니다. (2)

(1, 3) 구간에서 왼쪽 구간의 값 + 오른쪽 구간의 값을 반환합니다. (5 + 2)

(1,6)의 오른쪽 자식 노드인 (4,6) 구간이 (2,5) 구간과 겹치는 부분이 있어 왼쪽 자식 노드를 봅니다.

(4,5) 구간이 (2,5) 구간 안에 포함되어 있기 때문에 현재 구간의 값을 반환합니다. (10)

(1,6)의 오른쪽 자식 노드인 (6,6) 구간이 (2,5) 구간과 겹치는 부분이 없어 0을 반환합니다.

(4,6) 구간에서 왼쪽 구간의 값 + 오른쪽 구간의 값을 반환합니다. (10 + 0)

(1,6) 구간에서 왼쪽 구간의 값 + 오른쪽 구간의 값을 반환합니다. (7 + 10)

query(1,1,6,2,5)가 17을 반환하여 구간 합을 구할 수 있습니다!

<br/>

```cpp
struct SegmentTree {
	int* tree;
	int tree_size;
    SegmentTree(){}
	SegmentTree(int n) {
		tree_size = 1 << ((int)ceil(log2(n)) + 1);
		tree = new int[tree_size]();
	}
	int init(int* arr, int now, int start, int end) {
		if (start == end)
			return tree[now] = arr[start];
		int mid = (start + end) / 2;
		return tree[now] = init(arr, now * 2, start, mid) + init(arr, now * 2 + 1, mid + 1, end);
	}
	void update(int now, int start, int end, int idx, int val) {
		if (start > idx || idx > end) return;
		if (start == end) tree[now] = val;
		else {
			int mid = (start + end) / 2;
			update(now * 2, start, mid, idx, val);
			update(now * 2 + 1, mid + 1, end, idx, val);
			tree[now] = tree[now * 2] + tree[now * 2 + 1];
		}
	}
	int query(int now, int start, int end, int left, int right) {
		if (end < left || right < start) return 0;
		if (left <= start && end <= right) return tree[now];
		int mid = (start + end) / 2;
		return query(now * 2, start, mid, left, right) + query(now * 2 + 1, mid + 1, end, left, right);
	}
	~SegmentTree() {
		delete[] tree;
	}
};
```



---
<br/>

## BOTTOM-UP

<br/>

TOP-DOWN 방식과 다르게 루트 노드가 아닌 리프 노드에서부터 update, query 함수가 동작합니다.



구조체 구조부터 보겠습니다.



```cpp
struct SegmentTree {
	int* tree;
	int leaf;       // 세그먼트 트리의 가장 왼쪽 리프 노드의 인덱스
	SegmentTree(){
	void init(int* arr, int n) {}
	void update(int idx, int val) {}
	int query(int left, int right) {}
	~SegmentTree() {}
};
```

<br/>

tree_size 대신 leaf 변수가 추가되었습니다.

BOTTOM-UP 방식은 리프 노드부터 동작하기 때문에 리프 노드가 시작하는 인덱스를 알아야 합니다.

leaf를 구하는 식은 2^ceil(log(n))입니다.

세그먼트 트리는 완전 이진 트리여서 리프 노드의 개수가 나머지 노드들의 개수보다 1개가 더 많습니다.

그러므로 트리의 사이즈는 leaf(트리의 가장 왼쪽 리프 노드 인덱스) * 2입니다.

<br/>

```cpp
SegmentTree(int n) {
	leaf = (1 << ((int)ceil(log2(n))));
	tree = new int[leaf * 2]();
}
```

<br/>

트리를 생성할 때 leaf 값을 저장하고 tree를 leaf * 2 만큼 할당해줍니다.

<br/>

```cpp
void init(int* arr, int n) {
	for (int i = leaf; i < leaf + n; i++)
		tree[i] = arr[i - (leaf - 1)];
	for (int i = leaf - 1; i > 0; i--)
		tree[i] = tree[i * 2] + tree[i * 2 + 1];
}
```

<br/>

저는 arr 배열을 arr[1]부터 사용하여 arr[0]을 사용하지 않았기 때문에 arr 배열에서 (leaf - 1)을 하였습니다.

우선 리프 노드들을 입력 배열 arr의 값으로 저장을 해줍니다.

<br/>

**그리고 루트에서부터 양쪽 자식들의 구간 합을 저장하면 자식들의 값이 저장되어 있지 않으므로**

**리프 노드의 바로 위 트리 높이에서부터 루트까지 올라가며 구간 합들을 저장합니다.**

<br/>

![bottom-up init 함수 동작](https://i.imgur.com/zZdnLZ8.png)

<br/>

```cpp
void update(int idx, int val) { // idx - 값을 변경하고 싶은 인덱스, val - 변경할 값
	idx += (leaf - 1);
	tree[idx] = val;
	while (idx /= 2)
		tree[idx] = tree[idx * 2] + tree[idx * 2 + 1];
}
```

<br/>

update 함수가 TOP-DOWN 방식보다 간단합니다.

idx의 값을 세그먼트 트리에서 idx의 리프 노드 위치로 저장합니다. (arr[1]부터 시작했기 때문에 leaf - 1)

그다음 리프 노드의 값을 val로 바꿔줍니다.

이제 부모 노드로 가면서 구간의 합을 다 갱신을 해줄 겁니다.

**인덱스 / 2를 하면 부모 노드 인덱스를 구할 수 있으므로 idx가 0이 될 때까지 구간 합을 갱신**합니다.

<br/>

arr[7] = {0,1,6,2,7,3,2}에서 arr[2]을 5로 바꾸는 예제를 그림으로 보겠습니다.

<br/>

![bottom-up update 함수 동작](https://i.imgur.com/ycXHYj5.png)

<br/>

```cpp
int query(int left, int right) {  // left - 구하려는 구간 중 시작 인덱스, right - 구하려는 구간 중 끝 인덱스
	int ret = 0; // 구간 합 저장
	left += (leaf - 1), right += (leaf - 1);  // 리프 노드로 이동
	for (; left < right; left /= 2, right /= 2) {
		if (left % 2) ret += tree[left++];
		if (!(right % 2)) ret += tree[right--];
	}
	if (left == right) ret += tree[left];
	return ret;
}
```

<br/>

query 함수도 리프 노드에서 올라가면서 구간 합을 구합니다.

left, right를 리프 노드에서부터 시작해야 하니 (leaf - 1)을 더해줍니다.

반복문 안에 처리는 (2,6)의 구간 합을 구하는 그림을 보면서 설명하겠습니다.

<br/>

![bottom-up query 함수 동작](https://i.imgur.com/F18e7Kd.png)

<br/>

left에서 부모 노드로 올라가면서 구간 합을 구해줄 건데 구간이 1부터인 경우는 부모 노드 구간이 1을 포함하기 때문에

따로 처리를 안 해줘도 되지만 2인 경우에는 부모 노드 구간 (1,2)이 필요 없는 (1,1)의 구간도 포함하고 있기 때문에

아무 처리 없이 부모 노드로 가면 안 됩니다. 그래서 **left가 오른쪽에 있을 때 값을 ret에 저장해준 뒤 left++**을 하여 3으로 가줍니다.

right에서 부모 노드로 올라가면서 구간 합을 구할 때는 구간의 끝이 6인 경우에는

바로 부모로 올라가도 (5,6) 구간 안에 포함되지만 5인 경우에는 필요 없는 (6,6) 구간의 값이 있기 때문에

**left와 반대로 왼쪽에 있을 때 right--** 을 해준 뒤 부모 노드로 올라갑니다.

<br/>

(2, 6)를 구하는 과정을 설명하겠습니다.

left = (2, 2) 구간, right = (6,6) 구간에서 시작합니다.

left가 오른쪽에 있으므로 ret += tree[left]를 해준 뒤 left++을 합니다.

right는 왼쪽에 있으니 그대로 둡니다. 

left = (3,3), right = (6,6), ret = 5

반복문이 한번 돌아서 left, right 둘 다 부모 노드로 올라갑니다.

 left = (3,4), right = (5,6) ret = 5

left가 오른쪽에 있으므로 ret += tree[left]를 해준 뒤 left++을 합니다.

right는 오른쪽에 있으니 ret += tree[right]를 해준 뒤 right--를 합니다.

left = (5,6), right = (3,4), ret = 5 + 9 + 5 = 19

left < right 조건에 맞지 않으므로 반복문을 빠져나옵니다.

만약 left와 right가 같다면 마지막 구간 값을 더해줍니다.

구간 합이 저장되어 있는 ret를 반환합니다.

<br/>

```cpp
struct SegmentTree {
	int* tree;
	int leaf;
	SegmentTree(){}
	SegmentTree(int n) {
		leaf = (1 << ((int)ceil(log2(n))));
		tree = new int[leaf * 2]();
	}
	void init(int* arr, int n) {
		for (int i = leaf; i < leaf + n; i++)
			tree[i] = arr[i - (leaf - 1)];
		for (int i = leaf - 1; i > 0; i--)
			tree[i] = tree[i * 2] + tree[i * 2 + 1];
	}
	void update(int idx, int val) {
		idx += (leaf - 1);
		tree[idx] = val;
		while (idx /= 2)
			tree[idx] = tree[idx * 2] + tree[idx * 2 + 1];
	}
	int query(int left, int right) {
		int ret = 0;
		left += (leaf - 1), right += (leaf - 1);
		for (; left < right; left /= 2, right /= 2) {
			if (left % 2) ret += tree[left++];
			if (!(right % 2)) ret += tree[right--];
		}
		if (left == right) ret += tree[left];
		return ret;
	}
	~SegmentTree() {
		delete[] tree;
	}
};
```

---
<br/>



TOP-DOWN과 BOTTOM-UP 방식을 알아봤는데 저는 lazy propagation 문제를 풀 때는 TOP-DOWN으로 하고

기본 세그먼트 트리 문제 풀 때는 그때마다 하고 싶은 구현 방식으로 코딩합니다.

~~재귀를 좋아하는 편이라 TOP-DOWN을 자주 사용합니다..~~

<br/>

## 연습 문제) 구간 합 구하기

세그먼트 트리를 배워봤으니 백준에서 기본 문제 하나만 풀어보겠습니다.

<br/>

**[BOJ 2042 구간 합 구하기](https://www.acmicpc.net/problem/2042)**

<br/>

저희가 여태까지 위에서 공부했던 구간 합 구하는 세그먼트 트리를 그대로 구현하면 되는 문제입니다.

문제에도 long long을 쓰라고 했으니 꼭 쓰세요... ~~문제 대충 읽다가 int 써서 한번 틀렸습니다...~~

<br/>

```cpp
#include <cstdio>
#include <cmath>

typedef long long ll;

struct SegmentTree {
	ll* tree;
	int tree_size;
	SegmentTree(int n) {
		tree_size = (1 << ((int)ceil(log2(n)) + 1));
		tree = new ll[tree_size]();
	}
	ll init(ll* arr, int now, int start, int end) {
		if (start == end)
			return tree[now] = arr[start];
		int mid = (start + end) / 2;
		return tree[now] = init(arr, now * 2, start, mid) + init(arr, now * 2 + 1, mid + 1, end);
	}
	void update(int now, int start, int end, int idx, ll val) {
		if (start > idx || idx > end) return;
		if (start == end) tree[now] = val;
		else {
			int mid = (start + end) / 2;
			update(now * 2, start, mid, idx, val);
			update(now * 2 + 1, mid + 1, end, idx, val);
			tree[now] = tree[now * 2] + tree[now * 2 + 1];
		}
	}
	ll query(int now, int start, int end, int left, int right) {
		if (end < left || right < start) return 0;
		if (left <= start && end <= right) return tree[now];
		int mid = (start + end) / 2;
		return query(now * 2, start, mid, left, right) + query(now * 2 + 1, mid + 1, end, left, right);
	}
	~SegmentTree() {
		delete[] tree;
	}
};

int main() {
	int n, m, k;
	scanf("%d %d %d", &n, &m, &k);
	SegmentTree st(n);
	ll* arr = new ll[n + 1];
	for (int i = 1; i <= n; i++)
		scanf("%lld", &arr[i]);
	st.init(arr, 1, 1, n);
	for (int i = 1, x; i <= m + k; i++) {
		scanf("%d", &x);
		ll a, b; 
		scanf("%lld %lld", &a, &b);
		if (x == 1) 
			st.update(1, 1, n, a, b);
		else 
			printf("%lld\n", st.query(1, 1, n, a, b));
	}
	return 0;
}
```

<br/><br/>

세그먼트 트리를 배웠으니 다음에는 다른 구간 트리인 펜윅 트리나 lazy propagation을 할까 생각 중입니다... 음...

수고하셨습니다!

<br/>

![](https://media.giphy.com/media/U2REzyBrR6JPDtkYyQ/giphy.gif)