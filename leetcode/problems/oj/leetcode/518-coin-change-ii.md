#背包问题 #动态规划 #计数 
[518. 零钱兑换 II - 力扣（LeetCode）](https://leetcode.cn/problems/coin-change-ii/submissions/709056769/)

>第一版-速通
```python
class Solution:
    def change(self, amount: int, coins: List[int]) -> int:
        dp = [0] * (amount + 1)
        dp[0] = 1
        for i in coins:
            for j in range(i, amount + 1):
                dp[j] = dp[j] + dp[j - i]
        return dp[amount]
```