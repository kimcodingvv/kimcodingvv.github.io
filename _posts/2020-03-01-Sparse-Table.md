---
layout: post
title : "스파스 테이블 (Sparse Table, 희소 테이블)"
excerpt : "스파스 테이블을 알아보자!"
date : 2020-03-01-03:49
tags : [RMQ, Sparse Table]
category : [Algorithm]
comments : true
author: Kimcoding
feature: https://i.imgur.com/v9OSUmY.png
no-repeat : true
catalog : true
---



## 스파스 테이블이란?

<br/>



조건 1. arr에 저장된 값이 변하지 않는다.

조건 2. f(a, b, c) = f(a, (b, c)) = f(f(a, b),c)로 결합 법칙이 성립한다.

<br/>

배열 arr와 f 쿼리가 위 조건을 만족할 때 쿼리를 **O(lgN)** 만에 처리할 수 있는 자료 구조입니다.



---

<br/>

## 그거 왜 배워요...?



<br/>

구간 쿼리를 할 때 **f(a, b, c) = f(f(a, b), f(b, c))를** 만족하면 쿼리를 **O(1)**에 처리할 수 있습니다.

그래서 세그먼트 트리가 O(lgN) 만에 쿼리를 구할 수 있지만

스파스 테이블이 O(1) 만에 처리를 할 수 있는 쿼리들도 있어 사용한다고 합니다.

<br/>

그 외 LCA에 스파스 테이블을 사용하기도 하고

스파스 테이블을 이용하면 코드가 많이 짧아진다고 사용하기도 하네요.

<br/>

단, arr가 변하지 않아야 하므로

범용성이 떨어진다고 합니다 ㅠ



---

<br/>



## 스파스 테이블 전처리 과정



<br/>



구간 최솟값을 구하는 쿼리가 있을 때 스파스 테이블을 구현해보겠습니다.

arr[10] = {1,5,8,3,2,6,7,9,10,4}

f(l, r) = arr[l] ~ arr[r] 구간의 최솟값

<br/>

f(l, r)을 구한다고 했을 때 l~r 구간을 쭉 보면서 최솟값을 구하게 되면 O(N)의 시간이 걸립니다.

<br/>

이를 줄이기 위해 구간마다 최솟값을 저장하려고

Min[l][r]에 값을 저장하게 되면 O(1) 만에 값을 구할 수 있지만

Min을 저장하는 전처리가 O($$N^2$$), 메모리가 O($$N^2$$)라서 효율적이기 못합니다.

<br/>

**그럼 어떻게 해야 할까요??**

<br/>

Min[l][r] 대신 최솟값을 저장하는 Min 배열을 다르게 사용하겠습니다.

<br/>

**$$Min[i][j] = i \sim i + 2^j - 1 구간의 최솟값$$**

<br/>

이렇게 사용하겠습니다.

$$i + 2^j - 1$$ < $$N$$에서 j는 2의 지수이기 때문에 i = 0 일 때 j는 최대 $$log_2 (N-1)$$입니다.

그래서 Min 배열의 공간 복잡도는 O(NlgN)입니다.

<br/>

저 배열에 값들을 채워야 하는데 어떻게 구할까요?

<br/>

일단 Min[i][0] (0 < i < N)은 구간에 자기 자신밖에 없기 때문에 arr[i]와 같습니다.

<br/>

1 <= j <= $$log_2(N - 1)$$는 밑에 식으로 구할 수 있습니다.

<br/>

**$$Min[i][j] = min (Min[i][j - 1], Min[i + 2^{j-1}][j - 1])$$**

<br/>

j는 2의 지수여서 j -1을 하면 구간을 반으로 나눌 수 있습니다. $$(2^{j-1} + 2^{j-1} = 2^j)$$

$$i \sim i + 2^j - 1 = min( i \sim i + 2^{j-1} - 1, i + 2^{j-1} \sim  i + 2^j-1 + 2^{j-1} - 1)$$
$$= min( i \sim i + 2^{j-1} - 1, i + 2^{j-1} \sim  i + 2^j - 1)$$

<br/>

구하고자 하는 구간을 반으로 나누어 왼쪽 구간의 최솟값과 오른쪽 구간의 최솟값을 비교하여

둘의 최솟값을 저장해 주면 구하고자 하는 구간의 최솟값을 구할 수 있습니다.

<br/>

```cpp
int MAX = (int)log2(N - 1);
for (int i = 0; i < N; i++)
	Min[i][0] = arr[i];
for (int j = 1; j <= MAX; j++)
	for (int i = 0; i < N; i++)
		Min[i][j] = min(Min[i][j - 1], Min[i + (1 << (j - 1))][j - 1]);
```

<br/>

이렇게 Min 배열을 구하면 전처리 과정도 O(NlgN) 만에 할 수 있습니다.

<br/>

---

<br/>



## O(lgN) Query



<br/>

구간 최솟값 찾는 것은 O(1)도 가능하다고 했지만

O(1)가 안되는 쿼리들이 있으니 먼저 O(lgN)로 찾아보겠습니다.

<br/>

f(l, r)이 주어졌습니다.

저희는 $$i \sim i + 2^j - 1$$ 꼴의 구간 최솟값만 저장을 하였습니다.

<br/>

그렇다면 그 값들을 쓸 수 있게 만들어보겠습니다!

<br/>

l ~ r의 구간을 구하는 것이므로 구간 길이는 r - l + 1입니다.

이 인덱스 차이를 $$2^k$$ 들의 합으로 바꿔주겠습니다.

<br/>

$$2^a + 2^b + 2^c$$ 가 인덱스 차이라고 해봅시다.

그렇다면 $$l + 2^a + 2^b + 2^c = r + 1$$입니다.

$$f(l, r) = f(l, l + 2^a - 1) + f(l + 2^a, l + 2^a + 2^b - 1) + f(l + 2^a + 2^b , l + 2^a + 2^b + 2^c - 1)$$

$$= f(l, l + 2^a - 1) + f(l + 2^a, l + 2^a + 2^b - 1) + f(l + 2^a + 2^b , r)$$

**$$= Min[l][a] + Min[l + 2^a][b] + Min[l + 2^a + 2^b][c]$$**

<br/>

위처럼 구할 수 있습니다.

<br/>

2의 거듭제곱의 합으로 나타내기 위해 비트를 이용하여 간단하게 하겠습니다

<br/>

```cpp
int len = r - l + 1, MAX = (int)log2(N - 1), ans = 1e9;
for (int i = 0, j = l; i <= MAX; i++)
	if (len & (1 << i)) {
		ans = min(ans, Min[j][i]);
		j = j + (1 << i);
	}
```

<br/>

구간 길이 len 과 $$2^i$$ 를 and 연산을 해줘서 $$2^i$$ 가 2의 거듭제곱의 합에 포함되는지 확인한 후

포함되면 최솟값을 비교해 주고 $$j = j + 2^i$$ 를 하여 다음 구간을 봅니다.

<br/>

![](https://i.imgur.com/7TpFLEN.png)

<br/>

l = 2, r = 6, len = 5입니다.

len은 보기 편하게 $$101_2$$ 로 표현하겠습니다.

<br/>

i = 0 일 때 조건을 만족하기 때문에 ans와 Min[j][i] 값을 비교하여 최솟값을 저장합니다.

$$Min[2][0] = (2, 2 + 2^0 - 1) = (2, 2)$$ 구간의 최솟값

<br/>

(2, 2) 구간을 봤으니 (3, 6) 구간의 최솟값을 비교해 주면 됩니다.

$$j += 2^i$$ 를 하여 겹치지 않게 다음 구간을 봐줍니다.

<br/>

![](https://i.imgur.com/6AzWLBX.png)

<br/>

i = 2 일 때 조건을 만족하니 ans와 Min[j][i] 값을 비교하겠습니다.

$$Min[3][2] = (3, 3 + 2^2 - 1) = (3, 6)$$ 구간의 최솟값

<br/>

$$j += 2^i$$를 하고 더 이상 2의 거듭제곱 형태가 없으니 종료합니다.

<br/>

이런 식으로 하면 O(lgN)로 쿼리 처리를 할 수 있습니다.

<br/>

---

<br/>

## O(1) Query



<br/>



O(1)이라니 매우 끌립니다.

O(1)의 시간 복잡도는 f(a, b, c) = f(f(a, b), f(b, c))의 결합법칙이 성립해야 하는데

최솟값, 최댓값은 성립하니 구해보겠습니다.

<br/>

f(l, r)를 구하려고 합니다.

f(l, r) = f(a, b) + f(c, d) 형태로 만들려고 하는데 최솟값은 b >= c 여도 상관없습니다.

<br/>

범위가 겹쳐도 상관없으니 $$l + 2^x <= r$$를 만족하는 **가장 큰 x**를 찾겠습니다.

**$$x = floor(log_2(r - l + 1))$$**

<br/>

$$f(l, r) = f(l, l + 2^x - 1) + (r - 2^x + 1, r)$$ 이면 가장 큰 x를 구했기 때문에

무조건 겹치는 부분이 있지만 결괏값에 영향을 주지 않아 값을 구할 수 있습니다.

<br/>

![](https://i.imgur.com/v9OSUmY.png)

<br/>

그러므로

**$$ans = min( Min[l][x], Min[r - 2^x+ 1][x])$$**

<br/>

```cpp
int x = (int)log2(r - l + 1);
int ans = min(Min[l][x], Min[r - (1 << x) + 1][x]);
```

---

<br/>



LCA 글을 올리려고 sparse table을 먼저 올렸는데

매우 간단하게 하려고 했는데 생각보다 길어졌네요...

<br/>

글을 못쓰기도 하고 설명도 잘 못해서... ㅠ



<br/>



## 연습 문제

<br/>

**[BOJ 17435 합성함수와 쿼리](https://www.acmicpc.net/problem/17435)**

<br/>

여기까지 읽어주셔서 너무 감사합니다!

수고하세요!


