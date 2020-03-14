---
layout: post
title : "펜윅 트리 (Fenwick Tree, BIT)"
excerpt : "펜윅 트리를 알아보자!"
date : 2020-02-07-23:26
tags : [Segment Tree, Fenwick Tree]
category : [Algorithm]
comments : true
author: Kimcoding
feature: https://i.imgur.com/qDb0RDi.png
no-repeat : true
catalog : true
---



## 펜윅 트리란?

<br/>



**펜윅 트리,** **Binary Indexed Tree**라고도 하며 줄여서 **BIT**로도 불립니다.

세그먼트 트리와 같이 구간 쿼리를 **O(lgn)** 만에 구할 수 있습니다.

이 글은 세그먼트 트리를 알고 있다는 전제하에 작성하겠습니다.

<br/>

**[세그먼트 트리](https://kimcodingvv.github.io/Segment_Tree/)**

<br/>

세그먼트 트리를 알고 펜윅 트리를 공부하면 이해가 더 쉽고 빠른 것 같아

먼저 세그먼트 트리를 공부하길 추천드리겠습니다. (물론 주관적인 생각...)



---

<br/>

## 그거 왜 배워요..??

<br/>



세그먼트 트리가 있는데 굳이 펜윅 트리를...?

펜윅 트리로 풀리는 문제들은 세그먼트 트리로 풀 수 있습니다.

시간 복잡도는 같지만 상숫값이 달라 가끔씩 펜윅으로만 시간 안에 풀리는 문제가 있다고 합니다.

그리고 펜윅 트리는 세그먼트 트리보다 메모리를 줄일 수 있고 코드도 간단합니다.



---

<br/>



## 그러면 펜윅 트리만 사용하면 되지 않나요..?



<br/>



펜윅 트리는 이처럼 세그먼트 트리보다 **메모리도 적게 쓰고 코드도 간단**합니다.

펜윅 트리는 구간 합 같은 것들을 구할 때는 구현이 간단하지만

**최솟값, 최댓값 등 구간 쿼리를 하려고 할 때는 세그먼트 트리보다 구현이 어렵다고 합니다.** (저는 한 번도 안 해봤습니다...)

저는 그래서 펜윅으로 구현을 간단하게 할 수 있을 때는 펜윅 트리를

펜윅으로 구현이 힘들 것 같을 때는 세그먼트 트리를 사용합니다.

<br/>

세그먼트 트리는 나중에 lazy propagation를 이용하여 구간 업데이트를 구할 수 있는데

펜윅 트리는 예전에는 구간 업데이트를 못하는 줄 알았는데 할 수 있다고 합니다.

나중에 한번 찾아서 공부해봐야겠습니다.



---

<br/>



## 펜윅 트리 구현



<br/>

세그먼트 트리와 구성이 똑같습니다.

<br/>

**구성**

<br/>

배열, update 함수, query 함수

<br/>

세그먼트 트리는 A ~ B의 구간 값을 저장해줬지만 펜윅 트리는 다릅니다.

<br/>

![](https://i.imgur.com/qDb0RDi.png)

<br/>

이런 식으로 구간 값을 저장하게 됩니다.

저 구간마다 배열에 저장을 해줄 건데

<br/>

![](https://i.imgur.com/ck08utY.png)

<br/>

이처럼 배열 인덱스 x에 x가 포함된 구간 값을 저장할 것입니다.

세그먼트 트리와 다르게 배열 인덱스를 n까지 사용하기 때문에 메모리도 줄일 수 있습니다.



```cpp
// 펜윅 트리 구조체 구조
struct FenwickTree {
	int* tree, tree_size;
	FenwickTree(){}
	void update(int idx, int diff) {}
	int query(int idx) {}
	~FenwickTree(){}
};
```

<br/>

코드 구성은 이렇게 됩니다. 이제 구간합을 구하는 펜윅 트리를 하나하나씩 구현해보겠습니다.



---

<br/>



## 펜윅 트리 함수



<br/>

먼저 생성자를 구현하겠습니다.



```cpp
// 생성자 구현
FenwickTree(int n) : tree_size(n) {
	tree = new int[tree_size + 1]();
}
```

<br/>

tree_size라는 변수에 원하는 크기 n을 넣어서 저장해줍니다.

그리고 tree에 동적할당을 tree_size + 1만큼 해줍니다.

1부터 배열 인덱스를 사용할 것이므로 1~n이 필요하기 때문에 +1을 해줍니다.



---

<br/>



**펜윅 트리의 update 함수를 구현해보겠습니다.**

<br/>

```cpp
// idx - update 하려는 인덱스, diff - (변경하고자 하는 값 - 원래 값)
void update(int idx, int diff) {
	while (idx <= tree_size) {
		tree[idx] += diff;
		idx += (idx & -idx);
	}
}
```

<br/>

코드가 정말 간단합니다!

<br/>

![](https://media.giphy.com/media/5VKbvrjxpVJCM/giphy.gif)

<br/>

update 함수를 이해하려면 비트를 알아야 합니다.

arr[9] = {?, 1,5,2,7,3,4,6,9}일 때 구간 값들을 보겠습니다.

<br/>

![](https://i.imgur.com/R2Mi6D3.png)

<br/>

이런 식으로 구간 값들이 저장되어 있을 때
arr[3] = 5로 변경하는 update 함수 동작 과정을 그림과 함께 설명하겠습니다.

<br/>

![](https://i.imgur.com/X2OWRRO.png)

<br/>

빨간색으로 되어 있는 값들만 변경을 하게 될 것입니다.

update 함수를 실행할 때 여기서 idx = 3, diff = (5 - 2)입니다.

<br/>

3번째 인덱스를 갱신할 때 3이 포함되어 있는 3, 1~4, 1~8의 구간 값들을 변경해야 합니다.

이때 3, 4, 8번 업데이트를 하려고 보니 규칙이 보입니다!

<br/>

이 수들을 이진법으로 나타내면 3(00112), 4(01002), 8(10002)이 되는데

**0011 -> 0100 -> 1000을 보면 오른쪽에서 제일 먼저 1이 등장하는 자릿수에 1을 더해주면**

**다음 갱신해야 할 구간 인덱스가 됩니다!!**

호오오오오오오오오

<br/>

그럼 저희는 가장 오른쪽에 있는 1의 위치를 알아내서 1을 더해주면서

인덱스가 tree_size가 넘어갈 때까지 값들을 갱신해주면 됩니다.

<br/>



**그런데 가장 오른쪽에 있는 1의 위치는 어떻게 알죠...?**

<br/>

1100의 비트를 반전 시키면 0011입니다.

반전 시키면 가장 오른쪽에 있는 0이 저희가 찾는 인덱스 일 것입니다.

반전 시킨 수에서 1을 더하게 되면 0100이 되고 반전시키기 전 1100과 AND 연산을 하면

저희가 원하던 가장 오른쪽에 있는 1의 자릿수를 찾을 수 있습니다.

이예에에ㅔ에에에에ㅔ

<br/>

그럼 비트를 반전하고 1을 더하면 되나요?

idx += (~idx + 1) & idx을 해도 되지만 (~idx+1) 값은 2의 보수의 값과 같습니다.

이진수는 음수를 2의 보수로 표현하기 때문에 -idx & idx로 나타낼 수 있습니다.

<br/>

**그러므로 idx += (-idx & idx)를 하게 되면 갱신해야 하는 구간 인덱스들이 나오게 됩니다!!**



---

<br/>

**이제 query 함수를 구현하겠습니다.**

<br/>

```cpp
int query(int idx) { // 1~idx까지 구간 합 구하기
	int ret = 0;  // return 하려는 구간 합
	while (idx) {
		ret += tree[idx];
		idx -= (idx & -idx);
	}
	return ret;
}
```

<br/>

query 함수도 정말 간단합니다.

update 함수와 비슷한데 idx에 더하던 식이 빼는 식으로 바뀌었습니다.

<br/>

arr[9] = {?, 1,5,5,7,3,4,6,9}에서 2~7의 구간 합을 구해보겠습니다.

<br/>

펜윅 트리의 쿼리는 2~7 같은 구간 합을 구하지 못하고 1에서 시작하는 구간 합만 구할 수 있으므로

먼저 1~7을 구한 후 1~1 구간을 빼면 저희가 원하는 구간 합을 구할 수 있습니다.

이래서 구간 합이 아닌 최솟값, 최댓값 같은 것을 찾을 때는 구현이 어렵습니다.

<br/>

![](https://i.imgur.com/9eRVSwq.png)

<br/>

1~7 구간 합을 구하겠습니다.

1~4, 5~6, 7의 구간 합을 구하게 되면 저희가 원하는 1~7 구간 합을 알 수 있습니다.

7 -> 6 -> 4로 가는 규칙은 update 함수와 비슷합니다.

7(1112) -> 6(1102) -> 4(1002) 가 되는데

가장 오른쪽에 있는 1의 자릿수에서 이번엔 1을 빼줍니다!

그래서 idx가 0일 때까지 idx를 이동하며 나오는 구간의 합을 다 더해주면 됩니다.

<br/>

그래서 update 함수와 비슷한 원리로 **idx -= (-idx & idx)를 하게 되면 다음 구간을 구할 수 있습니다.**

<br/>

그래서 1~7을 구하게 되면 6 + 7 + 18 = 31이 되고

1~1을 같은 방식으로 구하면 1이 나와서

31 - 1 = 30이 답이 됩니다.

<br/>

---

```cpp
struct FenwickTree {
	int* tree, tree_size;
	FenwickTree(int n) : tree_size(n) {
		tree = new int[tree_size + 1]();
	}
	void update(int idx, int diff) {
		while (idx <= tree_size) {
			tree[idx] += diff;
			idx += (idx & -idx);
		}
	}
	int query(int idx) {
		int ret = 0;
		while (idx) {
			ret += tree[idx];
			idx -= (idx & -idx);
		}
		return ret;
	}
	~FenwickTree(){
		delete[] tree;
	}
};

```


<br/><br/>


펜윅 트리를 배울 때 세그먼트 트리를 먼저 배워서 그런지 막힘없이 배웠었던 것 같습니다. 

코드가 간단해서 너무 편리해요 ㅎㅎ

<br/>

**[BOJ 2042 구간 합 구하기](https://www.acmicpc.net/problem/2042)**

<br/>

세그먼트 트리를 하며 풀었던 문제지만 펜윅 트리로 풀어봐도 좋을 것 같아요 ㅎㅎ

밑에는 구간 합 구하기 코드입니다.

<br/>

```cpp
#include <bits/stdc++.h>
#define FIO ios::sync_with_stdio(0), cin.tie(0), cout.tie(0)
using namespace std;

typedef long long ll;

struct FenwickTree {
	ll* tree;
	int tree_size;
	FenwickTree(int n) : tree_size(n) {
		tree = new ll[tree_size + 1]();
	}
	void update(int idx, ll diff) {
		while (idx <= tree_size) {
			tree[idx] += diff;
			idx += (idx & -idx);
		}
	}
	ll query(int a, int b) { return query(b) - query(a - 1); }
	ll query(int idx) {
		ll ret = 0;
		while (idx) {
			ret += tree[idx];
			idx -= (idx & -idx);
		}
		return ret;
	}
	~FenwickTree(){
		delete[] tree;
	}
};

int main() {
	FIO;
	int n, m, k;
	cin >> n >> m >> k;
	FenwickTree ft(n);
	for (int i = 1; i <= n; i++) {
		ll x; cin >> x;
		ft.update(i, x);
	}
	for (int i = 1; i <= m + k; i++) {
		ll a, b, c; cin >> a >> b >> c;
		if (a == 1) ft.update(b, c - ft.query(b, b));
		else cout << ft.query(b, c) << '\n';
	}
	return 0;
}
```

<br/><br/>

펜윅 트리로 구간 업데이트 구간 쿼리 하는 법도 있다고 해서 그건 따로 글을 쓸 것 같습니다.

여기까지 보시느라 수고하셨습니다 감사합니다!!





