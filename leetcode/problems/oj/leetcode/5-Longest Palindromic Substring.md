[Longest Palindromic Substring - LeetCode](https://leetcode.com/problems/longest-palindromic-substring/solutions/)

#字符串 

>第一版wrong
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        # 暴力
        n = len(s)
        ans = ""
        max_n = min(0, n)
        for i in range(n):
            l = 0
            while i - l > 0 and i + l < n and s[i - l] == s[i + l]:
                l += 1
            if 2 * l - 1 > max_n:
                max_n = 2 * l - 1
                ans = s[i - l + 1: i + l]
            if i + 1 < n and s[i] == s[i + 1]:
                l = 0
                while i - l > 0 and i + l + 1 < n and s[i - l] == s[i + l + 1]:
                    l += 1
                if 2 * l > max_n:
                    max_n = 2 * l
                    ans = s[i - l + 1: i + l + 1]
        return ans
```

>Gemini加等号通过

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        # 暴力
        n = len(s)
        ans = ""
        max_n = min(0, n)
        for i in range(n):
            l = 0
            while i - l >= 0 and i + l < n and s[i - l] == s[i + l]:
                l += 1
            if 2 * l - 1 > max_n:
                max_n = 2 * l - 1
                ans = s[i - l + 1: i + l]
            if i + 1 < n and s[i] == s[i + 1]:
                l = 0
                while i - l >= 0 and i + l + 1 < n and s[i - l] == s[i + l + 1]:
                    l += 1
                if 2 * l > max_n:
                    max_n = 2 * l
                    ans = s[i - l + 1: i + l + 1]
        return ans
```