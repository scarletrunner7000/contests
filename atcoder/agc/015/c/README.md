# AtCoder Grand Contest 015

## [AC][AGC015] C - Nuske vs Phantom Thnook

### 方針

青マスをノードと考え、行き来できる青マスをエッジでつなぐと、森を作ることができる。
するとクエリは、ある長方形領域内における森に含まれる木の本数を数える問題に帰着できる。

森のノードとエッジの数をそれぞれ `V`, `E` とすると、`(森に含まれる木の本数) = V - E` と表すことができる。
なぜなら、任意の木について、ノードとエッジの数をそれぞれ `V'`, `E'` とすると、`V' - E' = 1` が成り立つからである。

前計算として、長方形領域に含まれるノードとエッジの数の2次元累積和を計算（O( N M )）しておけば、各クエリを O( 1 ) で計算できる。


### 計算量

O( N M + Q )


### keywords

森, 森に含まれる木の本数, 2次元累積和

