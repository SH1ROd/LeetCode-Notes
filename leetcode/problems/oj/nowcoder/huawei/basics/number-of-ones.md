#位运算
[求int型正整数在内存中存储时1的个数_牛客题霸_牛客网](https://www.nowcoder.com/practice/440f16e490a0404786865e99c6ad91c9?tpId=37&tqId=21238&rp=1&sourceUrl=%2Fexam%2Foj%2Fta%3FtpId%3D37&difficulty=undefined&judgeStatus=undefined&tags=&title=)
```c++
#include <iostream>
using namespace std;

int main() {
    int a;
    cin >> a;
    int ans =0;
    int p=1;
    while(p<a){
        if((a&p)==p){
            ans++;
        }
        p=p<<1;
    }
    cout << ans << endl;
}
// 64 位输出请用 printf("%lld")
```

```python
n = int(input())
p = 1
cnt = 0
while(p < n):
    if n&p == p:
        cnt += 1
    p *= 2
print(cnt)
```

>输入记得转换类型
```python
n = int(input())
```