#输入 
[字符串最后一个单词的长度_牛客题霸_牛客网](https://www.nowcoder.com/practice/8c949ea5f36f422594b306a2300315da?tpId=37&tqId=21224&rp=1&sourceUrl=%2Fexam%2Foj%2Fta%3FtpId%3D37&difficulty=undefined&judgeStatus=undefined&tags=&title=)

```c++
#include <iostream>
using namespace std;

int main() {
    string s;
    getline(cin, s);
    int temp = -1;
    for(int i=0;i<s.length();i++){
        if(s[i]==' '){
            temp = i;
        }
    }
    cout << s.length() - temp - 1 << endl;
    return 0;
}
// 64 位输出请用 printf("%lld")
```

> getline(cin, s);