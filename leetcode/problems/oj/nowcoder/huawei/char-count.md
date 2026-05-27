#输入 
[计算某字符出现次数_牛客题霸_牛客网](https://www.nowcoder.com/practice/a35ce98431874e3a820dbe4b2d0508b1?tpId=37&tags=&title=&difficulty=0&judgeStatus=0&rp=1&sourceUrl=%2Fexam%2Foj%2Fta%3FtpId%3D37)
```c++
#include <iostream>
using namespace std;

int main() {
    string s;
    getline(cin, s);
    char c;
    cin >> c;
    int cnt = 0;
    // if (isalpha(c)){
    for(int i=0;i<s.length();i++){
        if(tolower(s[i]) == tolower(c)){
            cnt++;
        }
    }
    cout << cnt << endl;
    // }
}
// 64 位输出请用 printf("%lld")
```

> tolower(c)