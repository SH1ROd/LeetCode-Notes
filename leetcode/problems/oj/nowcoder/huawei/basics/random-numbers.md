#排序
[明明的随机数_牛客题霸_牛客网](https://www.nowcoder.com/practice/3245215fffb84b7b81285493eae92ff0?tpId=37&tqId=21226&rp=1&sourceUrl=%2Fexam%2Foj%2Fta%3FtpId%3D37&difficulty=undefined&judgeStatus=undefined&tags=&title=)
```c++
#include <iostream>
#include <set>
#include <vector>
#include<algorithm>
using namespace std;
bool cmp(int a, int b){
    return a < b;
}

int main() {
    int n;
    cin >> n;
    set<int> a;
    vector<int> v; 
    for(int i=0;i<n;i++){
        int temp;
        cin >> temp;
        if (!a.count(temp)){
            a.insert(temp);
            v.push_back(temp);
        }
    }
    sort(v.begin(), v.end(), cmp);
    for(int i=0;i<v.size();i++){
        cout << v[i] << endl;
    }
}
// 64 位输出请用 printf("%lld")
```

```python
n = int(input())
v = set()
a = []
for i in range(n):
    b = int(input())
    if b not in v:
        v.add(b)
        a.append(b)
a.sort()
for t in a:
    print(t)

```