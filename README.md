# bibouroku_atcoder
自分の備忘録。atcoderで使えるやつをreadmeにまとめる

# 出やすいアルゴリズム

|abc|c問題のアルゴリズム|d問題のアルゴリズム|
| ---- | ---- | ---- |
|400|式の変形|ダイクストラ法|
|401|前を足し、後ろを引く|場合分け|
|402|更新|数学|
|403|データごとのフラグと<br>すべてのデータのフラグを用意する|動的計画法|
|404|Union-Find|3<sup>n</sup>回の***全*** ***通*** ***り***|
|405|事前に求める|BFS|
|406|ランレングス圧縮|列ごとのフラグと行ごとのフラグ|
|407|計算|HW回の***全*** ***通*** ***り***|

重要度というのは私自身の数値です、100だと必須、1だといらないぐらいの感じです。

細かいことを言うと100だと***重要度 100***, 70以上だと*重要度 70*, その他だと重要度 4みたいになります。
# イモス法(imos)

# 迷った時のイモス

# 強すぎる。

aが{1, 2, 3}とかだとして、aの0から2番目を見たいとかそういう全体のうちの少しを使う時に使う。

b<sub>n</sub> = b<sub>n-1</sub> + a<sub>n</sub>

そしてb[参照する最後]-b[参照する最初]がそのうちの結果になる。

***重要度 100***

*タグ:合計,切り替え,sum,リスト,スワップ,swap,文字列入れ替え,入れ替え,事前に求める*

pythonのコード：
```python
a=[1,2,3]
b=[]
Counting=0
for i in a:
  b.append(i+Counting)
  Counting+=i
# --- Example --- #
print(b[2]-b[0])
```
c++のコード：
```cpp
#include <iostream>

int main() {
  int l=3;
  int a[100] = {1, 2, 3};
  int b[100];
  int Counting = 0;
  for(int i=0; i<l; i++) {
    b[i]=a[i]+Counting;
    Counting+=a[i];
  }
  // --- Example --- //
  printf("%d\n", b[2]-b[0]);
  return 0;
}
```

# 二分探索法

{0,1,2,3}の中で2はどこのうちに入るか、がわかる方法です。

pythonだとbisectが便利すぎる。

**重要度 80**

*タグ:リスト,search,サーチ,bisect,found,見つける*

pythonのコード(bisect)：
```python
import bisect
def search(array,num):
  return bisect.bisect(array,num)
# --- Example --- #
print(search([0, 1, 3, 5], 4)))
```
C++のコード(vector)：
```cpp
#include <iostream>
#include <vector>
using namespace std;
int search(std::vector<int> v, int num) {
  int l=0;
  int r=v.size()-1;
  while(l<=r) {
    int mid=l+(r-l)/2;

    if (v[mid] == num) {
      return mid;
    }
    else if(v[mid] > num) {
      r=mid-1;
    }
    else {
      l=mid+1;
    }
  }
  return l;
}
int main() {
  printf("%d\n", search({0, 1, 3, 5}, 4));
}
```

# Union Find

くっつけたりできるやつ。
pythonのコード：
```python
class UnionFind:
    def __init__(self, n):
        self.parent = list(range(n))
        self.size = [1] * n
        self.groupsnum = n

    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])  # 経路圧縮
        return self.parent[x]

    def unite(self, x, y):
        x_root = self.find(x)
        y_root = self.find(y)
        if x_root == y_root:
            return
        if self.size[x_root] < self.size[y_root]:
            x_root, y_root = y_root, x_root
        self.parent[y_root] = x_root
        self.size[x_root] += self.size[y_root]
        self.groupsnum -= 1

    def issame(self, x, y):
        return self.find(x) == self.find(y)

    def __str__(self):
        from collections import defaultdict
        groups = defaultdict(list)
        for i in range(len(self.parent)):
            groups[self.find(i)].append(i)
        return "\n".join(map(str, groups.values())) + f"\n{self.groupsnum} groups found."
```
***C++のコード(ATCODERでしか使えない)***
C++のコード：
```cpp
#include <iostream>
#include "atcoder/dsu.hpp"
int main() {
  atcoder::dsu uf(2);
  printf("%d\n",uf.same(0, 1)); // 0
  uf.merge(0, 1);
  printf("%d\n",uf.same(0, 1)); // 1
  return 0;
}
```
