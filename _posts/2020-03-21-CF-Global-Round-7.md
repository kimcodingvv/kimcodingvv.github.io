---
layout : post
title : "Codeforces Global Round 7"
category : [Codeforces]
excerpt : "Bad bad..."
tags : [PS, Codeforces Global Round, Div.1 + Div.2]
comments : true
date : 2020-03-21 11:23
feature: /assets/img/post/5.webp
author : Kimcoding
catalog : true

---



![](https://user-images.githubusercontent.com/57852139/78282788-cff89200-7557-11ea-8ffb-2731ffebb178.png)

<br/>

하하하하하하하핳하ㅏ...

뭘 한걸까요...

최근 코포는 아쉬움만 남네요...ㅠㅠ

---

<br/>

## A. Bad Ugly Numbers

<br/>
[A - Bad Ugly Numbers](https://codeforces.com/contest/1326/problem/A)

<br/>

알고리즘

+ 수학

<br/>

처음에는 감이 안 왔는데

2와 3을 적절히 섞으면 원하는 답을 얻을 수 있습니다.

저는 (N - 1)이 3의 배수이면 마지막에 3이 2개 나머지 2, 아니면 마지막에 3이 1개 나머지 2 로 숫자를 만들었습니다.


<br/>


```cpp
#include <bits/stdc++.h>
#define FIO ios::sync_with_stdio(0), cin.tie(0), cout.tie(0)
#define FOR(a,b,c) for(int a = (b); a <= (c); a++)
#define RFOR(a,b,c) for(int a = (b); a >= (c); a--)
#define all(x) (x).begin(), (x).end()
#define vi vector <int>
#define vvi vector <vi>
#define ll long long
#define vll vector <ll>
#define vvl vector <vll>
#define pii pair<int,int>
#define pll pair<ll,ll>
#define eb emplace_back
#define ep emplace
#define fs first
#define sd second
#define mod 998244353
#define EPS 1e-9
using namespace std;

int main() {
	FIO;
	int t; cin >> t; while (t--) {
		int n; cin >> n;
		if (n == 1) cout << -1 << '\n';
		else if ((n - 1) % 3) {
			FOR(i, 1, n - 1) cout << 2;
			cout << 3 << '\n';
		}
		else {
			FOR(i, 1, n - 2) cout << 2;
			cout << 3 << 3 << '\n';
		}
	}
	return 0;
}

```

---


<br/>

## B. Maximums

<br/>

[B - Maximums](https://codeforces.com/contest/1326/problem/B)

<br/>

알고리즘

+ 수학
+ 구현

<br/>

i번째 수에서 1~i-1의 최댓값을 빼면 입력값이 나오므로 반대로 최댓값을 구하면서 입력값에서 최댓값을 더하면 원래 배열을 얻을 수 있습니다.


<br/>

```cpp
#include <bits/stdc++.h>
#define FIO ios::sync_with_stdio(0), cin.tie(0), cout.tie(0)
#define FOR(a,b,c) for(int a = (b); a <= (c); a++)
#define RFOR(a,b,c) for(int a = (b); a >= (c); a--)
#define all(x) (x).begin(), (x).end()
#define vi vector <int>
#define vvi vector <vi>
#define ll long long
#define vll vector <ll>
#define vvl vector <vll>
#define pii pair<int,int>
#define pll pair<ll,ll>
#define eb emplace_back
#define ep emplace
#define fs first
#define sd second
#define mod 998244353
#define EPS 1e-9
using namespace std;

int main() {
	FIO;
	int n; cin >> n;
	int Max = 0;
	FOR(i, 1, n) {
		int x; cin >> x;
		cout << x + Max << ' ';
		Max = max(Max, x + Max);
	}
	return 0;
}
```

---

<br/>

## C. Permutation Partitions

<br/>

[C - Permutation Partitions](https://codeforces.com/contest/1326/problem/C)

<br/>

알고리즘

+ 수학
+ 그리디

<br/>

부분 수열의 최댓값 합이 최대가 되려면 배열에서 최댓값 K개를 골라서

그 최댓값들을 다른 부분 수열로 배치해주시면 됩니다.

<br/>

K개의 최댓값 사이의 값들은 어느 부분 수열에 들어가도 상관없으니 

그 부분의 개수를 세어 다 곱하게 되면 경우의 수를 구할 수 있습니다.

<br/>

```cpp
#include <bits/stdc++.h>
#define FIO ios::sync_with_stdio(0), cin.tie(0), cout.tie(0)
#define FOR(a,b,c) for(int a = (b); a <= (c); a++)
#define RFOR(a,b,c) for(int a = (b); a >= (c); a--)
#define all(x) (x).begin(), (x).end()
#define vi vector <int>
#define vvi vector <vi>
#define ll long long
#define vll vector <ll>
#define vvl vector <vll>
#define pii pair<int,int>
#define pll pair<ll,ll>
#define eb emplace_back
#define ep emplace
#define fs first
#define sd second
#define mod 998244353
#define EPS 1e-9
using namespace std;

int main() {
	FIO;
	int n, k; cin >> n >> k;
	vector <pii> v(n);
	FOR(i, 0, n - 1) cin >> v[i].fs, v[i].sd = i;
	sort(all(v));
	ll ans = 0;
	vector <bool> chk(n);
	FOR(i, 1, k) {
		ans += v[n - i].fs;
		chk[v[n - i].sd] = 1;
	}
	ll ans2 = 1;
	int pre = -1;
	RFOR(i, n - 1, 0) {
		if (chk[i]) {
			if (pre == -1) {
				pre = i;
				continue;
			}
			ans2 *= (pre - i);
			ans2 %= mod;
			pre = i;
		}
	}
	cout << ans << ' ' << ans2 << '\n';
	return 0;
}

```

