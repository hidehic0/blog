+++
date = '2024-12-19T14:57:07+09:00'
draft = false
title = 'ABC369-Eを解いてみた'
categories  = ["過去問精進"]
tags = ["ワーシャルフロイド","順列全探索","bit全探索"]
+++

[問題へのリンク](https://atcoder.jp/contests/abc369/tasks/abc369_e)

# 考察したこと

普通に$N<=400$だから、普通に考えられるのは、ワーシャルフロイド法だなと思った。
で橋を渡る部分は現在地を、取っておけば全然大丈夫だからこの部分はいい

ここで少し解説を見た、順列全探索を使用するみたい

あとはbit全探索使えばいいなと、思って実装したらACした。

# ACコード

ライブラリは抜粋してあります

```py
N, M = il()
G = create_array2(N, N, INF)
L = []

for i in range(N):
    G[i][i] = 0

for _ in [0] * M:
    u, v, t = il()
    u -= 1
    v -= 1

    G[u][v] = min(G[u][v], t)
    G[v][u] = min(G[v][u], t)

    L.append((u, v, t))

Q = ii()

for k in range(N):
    for cur in range(N):
        for nxt in range(N):
            G[cur][nxt] = min(G[cur][nxt], G[cur][k] + G[k][nxt])


def solve():
    K = ii()
    B = il(-1)

    result = INF

    for p in permutations(B):
        for bit in range(1 << K):
            cur = 0
            ans = 0
            for i in range(K):
                if bit & (1 << i):
                    ans += G[cur][L[p[i]][0]] + L[p[i]][2]
                    cur = L[p[i]][1]
                else:
                    ans += G[cur][L[p[i]][1]] + L[p[i]][2]
                    cur = L[p[i]][0]

            ans += G[cur][N - 1]
            result = min(result, ans)

    return result


for _ in [0] * Q:
    print(solve())
```

# 最後に

これの部分問題、キーエンス2024のDみたいな感じだったな
この場合ワーシャルフロイドで拡張したけど、順列全探索+bit全探索は結構出てくるんだなって思った
