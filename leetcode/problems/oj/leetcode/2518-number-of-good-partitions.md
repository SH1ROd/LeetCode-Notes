#背包问题 #动态规划 #计数 #容斥 #组合
[2518. 好分区的数目 - 力扣（LeetCode）](https://leetcode.cn/problems/number-of-great-partitions/)

>原始失败版
```python
class Solution:
    def countPartitions(self, nums: List[int], k: int) -> int:
        # dp[j]是和>j的方案数
        # dp[j]是和==j的方案数
        # dp[j] += dp[j -i]
        # a >= k
        # b = sum - a >= k
        MOD = 10 ** 9 + 7
        n = len(nums)
        sum_ = sum(nums)

        if sum_ < 2 * k:
            return 0

        dp = [0] * (sum_ + 1)
        dp[0] = 1

        for i in nums:
            for j in range(sum_, i - 1, -1):
                dp[j] += dp[j - i]

        total = 2 ** n % MOD
        return total - sum(dp[k:sum - k]) % MOD
```

>强行改正版
```python
class Solution:
    def countPartitions(self, nums: List[int], k: int) -> int:
        MOD = 10 ** 9 + 7
        n = len(nums)
        sum_ = sum(nums)
        if sum_ < 2 * k:
            return 0
        dp = [0] * (k + 1)
        dp[0] = 1
        for i in nums:
            for j in range(k - 1, i - 1, -1):
                dp[j] = (dp[j] + dp[j - i]) % MOD
        total = 2 ** n % MOD
        bad = sum(dp[0: k + 1]) % MOD
        return (total - 2 * bad % MOD + MOD) % MOD
        
```

>标准答案
```python
class Solution:
    def countPartitions(self, nums: List[int], k: int) -> int:
        MOD = 10**9 + 7
        total_sum = sum(nums)
        
        # 剪枝：不可能存在好分区
        if total_sum < 2 * k:
            return 0
        
        # dp[j]：和为 j（j < k）的子集个数
        dp = [0] * k
        dp[0] = 1
        
        for num in nums:
            for j in range(k - 1, num - 1, -1):
                dp[j] = (dp[j] + dp[j - num]) % MOD
        
        # 不合法：子集和 < k
        bad = sum(dp) % MOD
        
        # 总方案数
        total = pow(2, len(nums), MOD)
        
        # 答案 = 总数 - 不合法 * 2
        return (total - 2 * bad % MOD + MOD) % MOD
```

> 简方法论（核心版）
> 
> 1. **先想补集：不好算“满足条件”，就算“不满足条件”**
>     
> 2. **子集划分问题 → 直接转成“子集和 + 背包DP”**
>     
> 3. **只关心 `< k` → DP 只开到 k（不要开到 sum）**
>     
> 4. **利用对称性：A / B 等价 → 不合法 × 2**
>     
> 5. **dp[j] 只表示一件事：和恰好为 j 的方案数（不能混）**
>     
> 6. **公式优先写成：`答案 = 总数 - 不合法`**


>下一版本
```python

```