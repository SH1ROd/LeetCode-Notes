#哈希表 
[13. 罗马数字转整数 - 力扣（LeetCode）](https://leetcode.cn/problems/roman-to-integer/)

>初版pass
```c++
class Solution {
public:
    int romanToInt(string s) {
        map<char, int> mp;
        mp['I'] = 1;
        mp['V'] = 5;
        mp['X'] = 10;
        mp['L'] = 50;
        mp['C'] = 100;
        mp['D'] = 500;
        mp['M'] = 1000;
        int i = 0;
        int n = s.length();
        int ans = 0;
        while(i < n){
            if(i < n - 1 && mp[s[i]] < mp[s[i+1]]){
                ans = ans - mp[s[i]] + mp[s[i+1]];
                i+=2;
            }
            else{
                ans += mp[s[i]];
                i++;
            }
        }
        return ans;
    }
};
```

>GPT改进
```c++
class Solution {
public:
    int romanToInt(string s) {
        // ✅ 使用 unordered_map 代替 map，提高查找效率（O(1) 而不是 O(log n)）
        unordered_map<char, int> mp = {
            {'I', 1}, {'V', 5}, {'X', 10},
            {'L', 50}, {'C', 100}, {'D', 500}, {'M', 1000}
        };
        
        int ans = 0;
        int n = s.length();
        
        // ✅ 单次遍历字符串，线性时间 O(n)
        for (int i = 0; i < n; ++i) {
            // 若当前字符对应的数值比下一个小，则表示是“减法”情况（如 IV = 4, IX = 9）
            if (i + 1 < n && mp[s[i]] < mp[s[i + 1]])
                ans -= mp[s[i]];   // 减去当前值
            else
                ans += mp[s[i]];   // 否则正常加上当前值
        }
        
        // ✅ 返回最终结果
        return ans;
    }
};
```

 >宜均
```python
class Solution:
    def romanToInt(self, s: str) -> int:
        lst = list(s)
        total = 0 

        for i in range(len(lst)):
            if lst[i] == "I":
                lst[i] = 1
            elif lst[i] == "V":
                lst[i] = 5
            elif lst[i] == "X":
                lst[i] = 10
            elif lst[i] == "L":
                lst[i] = 50
            elif lst[i] == "C":
                lst[i] = 100
            elif lst[i] == "D":
                lst[i] = 500
            elif lst[i] == "M":
                lst[i] = 1000

        for i in range(len(lst)):
            if ((i + 1) < len(lst)) and (lst[i] < lst[i+1]):
                total -= lst[i]

            else:
                total += lst[i]

        return total
```

>GPT

```python
class Solution:
    def romanToInt(self, s: str) -> int:
        roman = {
            "I": 1,
            "V": 5,
            "X": 10,
            "L": 50,
            "C": 100,
            "D": 500,
            "M": 1000
        }

        total = 0

        for i in range(len(s)):
            # 如果下一個字母的值比較大，表示要減
            if i + 1 < len(s) and roman[s[i]] < roman[s[i + 1]]:
                total -= roman[s[i]]
            else:
                total += roman[s[i]]

        return total
```

>2026年3月8日
```python
class Solution:
    def romanToInt(self, s: str) -> int:
        ans = 0
        d = {'I':1, 'V':5, 'X':10, 'L':50, 'C':100, 'D':500, 'M':1000}
        for i, x in enumerate(s):
            if i < len(s) - 1 and d[x] < d[s[i + 1]]:
                ans -= d[x]
            else:
                ans += d[x]
        return ans

```