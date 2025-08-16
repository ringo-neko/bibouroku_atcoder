# bibouroku_atcoder
自分の備忘録。atcoderで使えるやつをreadmeにまとめる

# イモス法(imos)
aが{1, 2, 3}とかだとして、aの0から2番目を見たいとかそういう全体のうちの少しを使う時に使う。

b<sub>n</sub> = b<sub>n-1</sub> + a<sub>n</sub>

そしてb参照する最後-b参照する最初がそのうちの結果になる。

pythonのコード：
```python
a=[1,2,3]
Counting=0
for i in a:
  a.append(i+Counting)
  Counting+=i
```
c++のコード：
```cpp
#include <iostream>

int main() {
  int l=3;
  int a[100] = {1, 2, 3};
  int b[100];
  int Counting = 0;
  for(int i; i<l; i++) {
    b[i]=a[i]+Counting;
    Counting+=a[i];
  }
  return 1;
}
```
