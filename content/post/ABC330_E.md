+++
date = '2025-02-07T18:49:27+09:00'
draft = false
title = 'ABC330-Eを解いた'
categories  = ["過去問精進"]
tags = ["Mex"]
+++

[問題へのリンク](https://atcoder.jp/contests/abc330/tasks/abc330_e)

# 考察
mexだから、sortedsetあればいいよな、だけど制約が、$A_i <= 10^9$とか書いてある

どうしよう

ここで解説を少し見る

そっか、要素は、最大N個しか失なわれないから、要素は、0からN+1まで準備すればいいのか

で普通にmexの実装をしてACした

# ACコード
いつもpython使ってるけど気分で、C++で解いていた
コンテスト中じゃなくて良かった
```cpp
#include <bits/stdc++.h>
#include <map>
#include <set>
using namespace std;

// 型テンプレ
using ll = long long;
using ull = unsigned long long;

// マクロ

#define rep(i, n) for (ll i = 0; i < (int)(n); i++)
#define all(a) (a).begin(), (a).end()

const ll INF = pow(10, 18);
const string upperlist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
const string lowerlist = "abcdefghijklmnopqrstuvwxyz";
ll N, Q;
map<ll, ll> D;
set<ll> L;

int main() {
  cin >> N >> Q;
  vector<ll> A(N);

  rep(i, N) {
    cin >> A[i];
    D[A[i]]++;
  }

  for (ll i = 0; i <= N + 100; ++i) {
    if (D[i] == 0) {
      L.insert(i);
    }
  }
  while (Q--) {
    ll i, x;
    cin >> i >> x;
    i--;

    D[A[i]]--;

    if (D[A[i]] == 0) {
      L.insert(A[i]);
    }

    A[i] = x;
    D[x]++;

    if (D[x] == 1) {
      L.erase(x);
    }

    cout << *L.begin() << "\n";
  }
}
```

