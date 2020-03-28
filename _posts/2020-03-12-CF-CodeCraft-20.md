---
layout : post
title : "CodeCraft-20 (Div. 2)"
category : [Codeforces]
excerpt : "???"
tags : [PS, Codeforces]
comments : true
date : 2020-03-12 04:01
feature: /assets/img/post/3.webp
author : Kimcoding
catalog : true



---



![](https://user-images.githubusercontent.com/57852139/77829648-ad850400-7166-11ea-9f3a-abb9ee1bd8a4.png)

<br/>

2솔을 해서 슬펐다가 등수는 나쁘지 않아서 위로가 됐습니다

지금 생각하면 D부터 풀 껄 그랬네요...

<br/>

---

<br/>

## A. Grade Allocation

<br/>
[A - Grade Allocation](https://codeforces.com/contest/1316/problem/A)

<br/>

알고리즘

+ 구현

<br/>

평균은 항상 일정하게 유지해야 합니다.

다른 사람 점수를 한 사람에게 몰아줘도 평균은 유지되므로 배열 전체 합과 M을 비교하여 최솟값을 구하면 됩니다.

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
using namespace std;

int main() {
	FIO;
	int t; cin >> t; while (t--) {
		int n, m; cin >> n >> m;
		ll ans = 0;
		FOR(i, 1, n) {
			int x; cin >> x;
			ans += 1ll * x;
		}
		cout << min(ans, 1ll * m) << '\n';
	}
	return 0;
}
```

---


<br/>

## B. String Modification

<br/>

[B - String Modification](https://codeforces.com/contest/1316/problem/B)

<br/>

알고리즘

+ 완전 탐색

<br/>

N이 홀수일 때와 짝수 일때로 나눠서 규칙을 찾으면 됩니다.

1~N까지 K를 정해서 다 구해보는데 K 와 N이 홀수 일때는 K 기준으로 역순으로 넣어주고 둘 다 짝수 일때는 K기준으로 순서대로 넣어주면 됩니다.

자세한 구현은 코드를 참고해주세요!

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
using namespace std;

int main() {
	FIO;
	int t; cin >> t; while (t--) {
		int n, num; cin >> n;
		string s, ans; cin >> s;
		FOR(i, 1, 5005) ans += 'z';
		FOR(i, 1, n) {
			string a;
			FOR(j, i - 1, n - 1) a += s[j];
			if ((i & 1) == (n & 1)) {
				RFOR(j, i - 2, 0) a += s[j];
			}
			else FOR(j, 0, i - 2) a += s[j];
			if (a < ans) ans = a, num = i;
		}
		cout << ans << '\n' << num << '\n';
	}
	return 0;
}
```

---

<br/>

## C. Primitive Primes

<br/>

[C - Primitive Primes](https://codeforces.com/contest/1316/problem/C)

<br/>

알고리즘

+ 수학

<br/>

대회 때 한참 고민했는데 풀이를 듣고 그런 방법이...? 간단한 방법으로 풀립니다.

P로 나눴을 때 나머지가 0이면 안됩니다. 그러므로 P로 값들을 미리 모듈러 연산을 해줍니다.

그리고 a, b들이 0이 아닌 값이 처음 나온 인덱스를 구합니다.

그 둘을 더한 값이 답이 됩니다.

이유는 그 전까지 a, b가 0이었기 때문에 a 인덱스 뒤, b 인덱스 전을 곱해도 0이고, 반대로 해도 0이 되므로 둘 다 0이 아닌 값이 계수가 됩니다.

그러므로 정답이 될 수 있습니다.

<br/>

```cpp
#include <bits/stdc++.h>
#define FIO ios::sync_with_stdio(0), cin.tie(0), cout.tie(0)
#define FOR(i,a,b) for(int i=a;i<=b;i++)
#define vi vector <int>
#define vvi vector <vi>
#define eb emplace_back
using namespace std;

int main() {
	FIO;
	int n, m, p; cin >> n >> m >> p;
	int a[1000005], b[1000005];
	FOR(i, 0, n-1) {
		int x; cin >> x;
		a[i] = x % p;
	}
	FOR(i, 0, m-1) {
		int x; cin >> x;
		b[i] = x % p;
	}
	int ans = 0;
	FOR(i, 0, n-1) if (a[i]) {
		ans += i; break;
	}
	FOR(i, 0, m-1) if (b[i]) {
		ans += i; break;
	}
	cout << ans << '\n';
	return 0;
}
```

---

<br/>

## D. Nash Matrix

<br/>

[D - Nash Matrix](https://codeforces.com/contest/1316/problem/D)

<br/>

알고리즘

+ DFS
+ 시뮬레이션

<br/>

현 좌표와 멈추는 좌표가 같다면 그 자리는 X입니다.

X부터 멈추는 좌표가 같은 좌표들을 DFS하며 찾습니다.

DFS하면서 X부터 시작했기 때문에 역방향으로 길을 저장해줍니다.

<br/>

(-1,-1)이 있다면 (-1,-1)인 좌표들을  DFS로 찾아서 쭉 이어주고 마지막에 사이클을 만들어주면 됩니다.

정답이 다 완성되지 않았을 때는 INVALID를 출력하고 완성됐으면 VALID와 맵을 출력해주시면 됩니다.

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
using namespace std;

int main() {
	FIO;
	int n; cin >> n;
	pii map[1005][1005];
	int visit[1005][1005] = {};
	char ans[1005][1005] = {};
	FOR(i, 0, n - 1) FOR(j, 0, n - 1) {
		cin >> map[i][j].fs >> map[i][j].sd;
		if (i + 1 == map[i][j].fs && j + 1 == map[i][j].sd)
			ans[i][j] = 'X';
	}
	int d[4][2] = { {0,-1},{1,0}, {0,1},{-1,0} }, cnt = 0;
	char ch[4] = { 'R', 'U', 'L', 'D' };
	pii val;
	function <bool(int, int)> dfs = [&](int r, int c) {
		int k = 0;
		for (int i = 0; i < 4; i++) {
			int nr = r + d[i][0], nc = c + d[i][1];
			if (nr < 0 || nc < 0 || nr >= n || nc >= n) continue;
			if (map[nr][nc] != val) continue;
			if (visit[nr][nc]) continue;
			if (!ans[r][c]) ans[r][c] = ch[(i + 2) % 4];
			visit[nr][nc] = 1;
			ans[nr][nc] = ch[i];
			cnt++; k++;
			dfs(nr, nc);
		}
		return k > 0;
	};
	FOR(i, 0, n - 1) FOR(j, 0, n - 1) {
		if (visit[i][j]) continue;
		if (map[i][j] != pii(-1, -1) && ans[i][j] != 'X') continue;
		val = map[i][j];
		cnt++; visit[i][j] = 1;
		if(!dfs(i, j) && map[i][j] == pii(-1,-1))
			return cout << "INVALID" << '\n', 0;
	}
	if (cnt < n * n) return cout << "INVALID" << '\n', 0;
	cout << "VALID" << '\n';
	FOR(i, 0, n - 1) {
		FOR(j, 0, n - 1) cout << ans[i][j];
		cout << '\n';
	}
	return 0;
}
```

