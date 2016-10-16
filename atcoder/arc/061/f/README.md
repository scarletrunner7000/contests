# ARC 061

## F - 3人でカードゲーム / Card Game for Three [AC-]

### 方針

`a`, `b`, `c` のカードが場に捨てられる順番に着目し、場に捨てられたカードを1列に順番に並べて考えて、 combination の様々な公式を駆使して数え上げる。

A が勝つための必要十分条件は、`a` が N 回出るまでに出た `b`, `c` がそれぞれ M, K 回以下であることである。ここで、N 回目の `a` が出るのが p ターン目、N 回目で勝負が決したまでに `b` が出たのが q 回とする。このとき、求めるパターン数は、

$$
\sum_{p} {}_{p-1}{C}_{N-1} \times ( \sum_{q} {}_{p-N}{C}_{q} ) \times 3^{N + M + K - p} \\
( N \le p \le N + M + K) \\
(\max(0, p - N - K) \le q \le \min(p - N, M) )
$$

で表せる。ここで、上記の式の1行目の第1, 2, 3項をそれぞれ c0, c1, pow3 と呼ぶこととする。

c0, pow3 は p を1ずつ増やしながら順次計算できるのが、 c1 が面倒くさい。


```
          *
         * *
        * * *
       * * * *
      * * * * -
     - * * * - -
    - - * * - - -
   - - - * - - - -
  - - - - - - - - -
```

c1 は、上図のような、パスカルの三角形上の平行四辺形領域を考えたときの、 p - N 行目の和に相当する。各行の和を上から1行ずつ順次計算していく。1行下がるときに、

* 両側が増えるときは、前行の和を2倍する
* 片側が減るときは、前行の和を2倍したうえで前行の減る側の一番端にあった値を引く
* 両側が減るときは、前行の和を2倍したうえで前行の両側の一番端にあった値を引く

という計算を行えばいい。

参照:
[ABC045 / ARC061 解説](http://arc061.contest.atcoder.jp/data/arc/061/editorial.pdf)

#### その他

mod M の世界で除算をするときは、単に $A / B$ としてもうまくいかない。代わりに $A \cdot B^{-1}$ を考えればいい。

$B$ の逆元 $B^{-1}$ は、拡張ユークリッドの互除法で求めることができる。


### 計算量

O( M + K )


### keywords

combination, 組み合わせ, 数え上げ, mod, mod の除算, 逆元, 拡張ユークリッドの互除法, パスカルの三角形
