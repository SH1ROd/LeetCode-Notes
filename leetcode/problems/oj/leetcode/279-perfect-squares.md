#背包问题 #动态规划 #最优化
[279. 完全平方数 - 力扣（LeetCode）](https://leetcode.cn/problems/perfect-squares/description/)

>第一版通过
```python
class Solution:
    def numSquares(self, n: int) -> int:
        dp = [x for x in range(n + 1)]
        dp[1] = 1
        for i in range(1, int((n + 1) ** 0.5) + 1):
            for j in range(i ** 2, n + 1):
                dp[j] = min(dp[j], dp[j - i ** 2] + 1)
        return dp[n]
```

