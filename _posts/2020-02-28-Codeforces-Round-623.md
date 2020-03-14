---
layout : post
title : "Codeforces Round #623 (Div. 2)"
category : [Codeforces]
excerpt : "First 4 solve!!!"
tags : [Codeforces, Codeforces Round]
comments : true
date : 2020-02-28 23:03
feature: https://i.imgur.com/NudDYH6.png
no-repeat : true
author : Kimcoding
catalog : true
---

![](https://i.imgur.com/bxk3Ef3.png)

![](https://i.imgur.com/cdfC0EC.png)

<br/>


코드포스를 하며 처음으로 4솔을 했습니다

기하ㅏㅏㅏ학!
<br/><br/>

![](https://media.giphy.com/media/11sBLVxNs7v6WA/giphy.gif)

<br/><br/>
덕분에 처음으로 블루를 갔어요 ㅎㅎ

다음 코포에서 어떻게 될는지...
<br/>


---

<br/>

## ﻿A. Dead Pixel


<br/>
**[A - Dead Pixel](https://codeforces.com/contest/1315/problem/A)**

<br/>

a, b, x, y 가 입력으로 주어집니다.

a x b 격자가 주어졌을 때 (x, y)를 포함하지 않은 가장 큰 직사각형의 넓이를 구하면 됩니다.

<br/>

![](https://i.imgur.com/NudDYH6.png)
<br/>


```cpp
#include <bits/stdc++.h>
#define FIO ios::sync_with_stdio(0), cin.tie(0), cout.tie(0)
using namespace std;

int main() {
	FIO;
	int t; cin >> t; while (t--) {
		int a, b, x, y;
		cin >> a >> b >> x >> y;
		int ans;
		ans = max({ a * y, b * x, (a - 1 - x) * b, (b - 1 - y) * a });
		cout << ans << '\n';
	}
	return 0;
}
```

---


<br/>
## ﻿B. Homecoming
<br/>


[B - Homecoming](﻿https://codeforces.com/contest/1315/problem/B)

<br/>

문제가 간단해서 바로 코딩을 시작했는데
생각을 정리 안 하고 해서 그런지 아니면 구현력이 많이 부족한 건지...

구현을 하다가 계속 뇌 정지가 와서 오래 걸렸습니다...

뒤에서부터 보면서 버스를 탈 수 없을 때까지 보고
버스를 탈 수 없을 때 그곳까지 걸어가야 하니 그 인덱스를 구하였습니다.

제출할 때도 시스템 테스트할 때도
반례가 있을까 봐 조마조마했습니다.

다행...

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
#define pii pair<int,int>
using namespace std;
 
int main() {
	FIO;
	int t; cin >> t; while (t--) {
		int a, b, p;
		cin >> a >> b >> p;
		string s; cin >> s;
		int i = (int)s.size() - 2;
		for (;i >= 0;) {
			if (s[i] == 'A' && p < a) break;
			else if (s[i] == 'A' && p >= a) p -= a;
			if (s[i] == 'B' && p < b) break;
			else if (s[i] == 'B' && p >= b) p -= b;
			while (i && s[i] == s[i - 1]) i--;
			i--;
		}
		cout << i + 2 << '\n';
	}
	return 0;
}
```

---


<br/>
## ﻿C. Restoring Permutation
<br/>


[C - Restoring Permutation](﻿https://codeforces.com/contest/1315/problem/C)
<br/><br/>


그리디로 생각을 했습니다.


사전 순이므로 1~N까지 보면서
b[i] = min(a[2 * i - 1], a[2 * i])이므로

a[2 * i - 1] = b[i] 이어야 사전 순으로 앞서고
a[2 * i]은 b[i]보다 크고 현재까지 나오지 않은 수 중에 가장 작은 값을 넣어줬습니다.

<br/>

그렇게 하면 사전 순으로 가장 앞서는 순열을 구할 수 있습니다.

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
#define pii pair<int,int>
#define eb emplace_back
using namespace std;

int main() {
	FIO;
	int t; cin >> t; while (t--) {
		int n; cin >> n;
		bool chk[205] = {};
		vi ans, arr(n + 1);
		for (int i = 1; i <= n; i++) cin >> arr[i], chk[arr[i]] = 1;
		int flag = 0;
		for (int i = 1; i <= n; i++) {
			flag = 0;
			for (int j = arr[i] + 1; j <= 2 * n; j++) {
				if (chk[j]) continue;
				flag = 1;
				chk[j] = 1;
				ans.eb(arr[i]); ans.eb(j);
				break;
			}
			if (!flag) break;
		}
		if (!flag) {
			cout << -1 << '\n';
			continue;
		}
		for (int i : ans) cout << i << ' ';
		cout << '\n';
	}
	return 0;
}
```

---


<br/>
## ﻿D. Recommendations

<br/>

[﻿D - Recommendations](﻿https://codeforces.com/contest/1315/problem/D)
<br/><br/>


2시간 1분 일 때 풀었는데 2시간이었으면 3솔일뻔 했습니다...

다음부터는 구현 시간을 좀 줄여봐야겠네요.

<br/>

중복되는 카테고리의 간행물 수가 있다면
중복되지 않게 간행물을 찾아 더하는 문제입니다.

<br/>

일단 최솟값을 구하려면 중복되는 것들 중에 찾는 데 가장 오래 걸리는 것을 제외하고 나머지를 간행물을 한 개 더 찾으면 됩니다.

<br/>

정렬해서 가장 적은 간행물을 먼저 보면서 중복이 없을 경우는 무시하고 갑니다.

중복이 있을 경우 위에서 말한 것처럼 가장 오래 걸리는 것을 제외하고

나머지를 찾아야 하는 데 가장 오래 걸리는 것을 찾기 위해 map을 써서 최댓값을 구해줬고

나머지를 찾는 데 걸리는 시간을 더하기 위해 세그먼트 트리를 사용했습니다.

<br/>

이 과정을 중복이 없을 때, 끝까지 진행하면 답을 구할 수 있습니다.

<br/>

굳이 세그먼트 트리를 안 써도 될 것 같은데 최근에 저런 유형을 세그먼트 트리로 풀다 보니
생각나는 대로 풀었네요...
다른 분들의 풀이를 보니 우선순위 큐를 많이 사용하시는 것 같았습니다.

<br/>

그... 그래도 풀었으니까...?
하핳ㅎ

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
#define pii pair<int,int>
#define eb emplace_back
#define fs first
#define sd second
using namespace std;

struct ST {
	vll tree; int leaf;
	ST(int n) {
		leaf = (1 << (int)ceil(log2(n)));
		tree.resize(leaf * 2);
	}
	void update(int idx, ll val) {
		idx += leaf;
		tree[idx] = val;
		while (idx >>= 1) tree[idx] = tree[idx * 2] + tree[idx * 2 + 1];
	}
	ll query(int l, int r) {
		ll ret = 0;
		l += leaf, r += leaf;
		for (; l <= r; l >>= 1, r >>= 1) {
			if (l & 1) ret += tree[l++];
			if (~r & 1) ret += tree[r--];
		}
		if (l == r) ret += tree[l];
		return ret;
	}
	~ST() {
		tree.clear();
	}
};

map <pii, int> m;

int main() {
	FIO;
	int n; cin >> n;
	vector <pii> v(n);
	for (int i = 0; i < n; i++) cin >> v[i].fs, v[i].sd = i;
	sort(all(v));
	vi time(n);
	ST st(n);
	for (int i = 0; i < n; i++) cin >> time[i];
	int now = 0;
	ll ans = 0;
	for (int i = 0; i < n; i++) {
		while (m.size() && now < v[i].fs) {
			auto it = m.end(); --it;
			st.update(it->fs.sd, 0);
			ans += st.query(0,n - 1);
			now++;
			m.erase(it);
		}
		if (m.empty()) now = v[i].fs;
		st.update(v[i].sd, time[v[i].sd]); m[{time[v[i].sd], v[i].sd}] = 1;
		while (i < n - 1 && v[i].fs == v[i + 1].fs) {
			st.update(v[i + 1].sd, time[v[i + 1].sd]);
			m[{time[v[i + 1].sd], v[i + 1].sd}] = 1;
			i++;
		}
		auto it = m.end(); --it;
		st.update(it->fs.sd, 0);
		ans += st.query(0, n - 1);
		now++;
		m.erase(it);
	}
	while (m.size()) {
		auto it = m.end(); --it;
		st.update(it->fs.sd, 0);
		ans += st.query(0, n - 1);
		now++;
		m.erase(it);
	}
	cout << ans << '\n';
	return 0;
}
```

