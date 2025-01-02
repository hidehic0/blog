+++
date = '2025-01-02T16:59:39+09:00'
draft = false
title = 'ABC333-Eを解いた'
categories = ["過去問精進"]
tags = [ "Stack", "imos法" ]
+++
[問題へのリンク](https://atcoder.jp/contests/abc333/tasks/abc333_e)

# 考察したこと
使った場所は、必要になったら使うという貪欲で求めることが、できるので(公式解説の丸パクリ)あとは途中持っている**最大値**の**最小値**を求めるだけ
そちらは、imos法で、できるためあとは、ポーションをstackで管理すれば、OK

計算量は$O(N)$となり全然間に合う、ていうか、現在の環境だと、間に合わないとおかしい

# ACコード
ライブラリは抜粋してあります
[ライブラリ全文](https://github.com/hidehic0/library)
変数名がゴミすぎてすみません

```py
N = ii()
data = [0] * N
D = defaultdict(list)
ans = [0] * N
T = []

for i in range(N):
    t, x = il()
    T.append(t)

    if t == 1:
        D[x].append(i)
    elif t == 2:
        if len(D[x]) == 0:
            print(-1)
            exit()

        data[D[x][-1]] += 1
        data[i] -= 1
        ans[D[x][-1]] = 1
        D[x].pop()

ns = []

for i in range(N):
    if T[i] == 1:
        ns.append(ans[i])

print(max(list(accumulate(data))))
print(*ns)
```

# 感想
novistepsでstackの問題として見つけたけど、面白かった
