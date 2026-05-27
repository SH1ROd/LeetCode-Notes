#栈 
[括号的最大嵌套深度 - 力扣（LeetCode）](https://leetcode.cn/problems/maximum-nesting-depth-of-the-parentheses/description/)
```python
class Solution:
    def maxDepth(self, s: str) -> int:
        v = []
        cnt = 0
        ans = 0
        for c in s:
            if c == '(':
                v.append(c)
                cnt += 1
                ans = max(ans, cnt)
            elif c == ')':
                v.pop()
                cnt -= 1
        return ans
```