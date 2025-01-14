+++
date = '2025-01-14T11:33:04+09:00'
draft = true
title = 'ABC178-Dを解いた'
categories = ["過去問精進"]
tag = ["累積和", "DP"]
+++

[問題へのリンク](https://atcoder.jp/contests/abc178/tasks/abc178_d)

# 考察したこと
累積和dp?だと思った
まずSが2000以下というのが怪しいし、$2000/3 = 666.666...$なので、あとは、うまいこと遷移させればいいと思った
累積和のi-3の値を貰って、modを取れば遷移はOK
あとは、dp配列のインデックスがSの所の総和をMOD取った値を出力すればOK

普通に一次元配列で解く解法もあるみたいだけど、二次元配列で解いた

# ACコード
ライブラリは抜粋してあります
[ライブラリ全文](https://github.com/hidehic0/library)

```py
S = ii()
MOD = 10**9 + 7
dp = create_array2(701, S + 1, 0)
dp[0][0] = 1

for i in range(700):
    acc = list(accumulate(dp[i]))

    for k in range(3, len(dp[0])):
        dp[i + 1][k] += acc[k - 3]
        dp[i + 1][k] %= MOD

ans = 0

for i in range(len(dp)):
    ans += dp[i][S]
    ans %= MOD

print(ans)
```
