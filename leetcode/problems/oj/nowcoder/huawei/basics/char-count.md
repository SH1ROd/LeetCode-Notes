#哈希表 
[字符个数统计_牛客题霸_牛客网](https://www.nowcoder.com/practice/eb94f6a5b2ba49c6ac72d40b5ce95f50?tpId=37&rp=1&sourceUrl=%2Fexam%2Foj%2Fta%3FtpId%3D37&difficulty=&judgeStatus=&tags=&title=&gioEnter=menu)
```c++
#include <iostream>
#include <bits/stdc++.h>
using namespace std;

int main() {
    string s;
    getline(cin, s);
    int ans = 0;
    unordered_map<char, int> m;
    for(int i=0;i<s.size();i++){
        if(m.count(s[i])==0){
            ans++;
            m[s[i]] = 1;
        }
        else{
            m[s[i]] += 1;
        }
    }
    cout << ans << endl;
}
// 64 位输出请用 printf("%lld")
```

```python
s = input()
d = {}
cnt = 0
for c in s:
    d[c] = d.get(c, 0) + 1
    if d[c] == 1:
        cnt += 1
print(cnt)

```

>字典计数器写法
```python
d[c] = d.get(c, 0) + 1
```

>ord → order → 顺序值
```python
s = input()
v = set()
for c in s:
    c = ord(c)
    if c >= 0 and c <= 127:
        v.add(c)
print(len(v))

```