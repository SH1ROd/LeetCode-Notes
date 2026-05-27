#背包问题 #动态规划 #最优化
[322. 零钱兑换 - 力扣（LeetCode）](https://leetcode.cn/problems/coin-change/submissions/709054835/)

>第一版-五分钟速通
```python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [float('inf')] *(amount + 1)
        dp[0] = 0 
        for i in coins:
            for j in range(i, amount + 1):
                dp[j] = min(dp[j], dp[j - i] + 1)
        if dp[amount] == float('inf'):
            return -1
        return dp[amount]
```

