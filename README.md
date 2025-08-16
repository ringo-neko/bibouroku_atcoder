# bibouroku_atcoder
自分の備忘録。atcoderで使えるやつをreadmeにまとめる

# 初めに
実行速度を早くしたいなら、この表を見てメリット、デメリットを見るとよい。
ここでのdequeとは、collections.dequeというものとする。
| |リスト|deque|set|dict|
| ---- | ---- | ---- | ---- | ---- |
|要素を追加|O(1)|O(1)|O(1)|O(n)|
|最初に追加|O(n)|O(1)|できない|できない|
|消す|O(1)|O(1)|O(len(s))|O(n)|
|n番目を見る|O(1)|O(1)|できない|O(n)|
|コピー|O(n)|O(n)|O(n)|O(n)|
|含まれているか|O(n)|O(n)|O(1)|O(n)|
|メモリ|多め|多め|少なめ|少なめ|
|デメリット|ない|ない|ユニークな要素しか扱えない|見やすいが遅い|

重要度というのは私自身の数値です、100だと必須、1だといらないぐらいの感じです。

細かいことを言うと100だと***重要度 100***, 70以上だと*重要度 70*, その他だと重要度 4みたいになります。
# イモス法(imos)

# 迷った時のイモス

# 強すぎる。

aが{1, 2, 3}とかだとして、aの0から2番目を見たいとかそういう全体のうちの少しを使う時に使う。

b<sub>n</sub> = b<sub>n-1</sub> + a<sub>n</sub>

そしてb[参照する最後]-b[参照する最初]がそのうちの結果になる。

***重要度 100***

*タグ:合計,切り替え,sum,リスト,スワップ,swap,文字列入れ替え,入れ替え*

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
