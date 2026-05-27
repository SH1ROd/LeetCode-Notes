#背包问题 #动态规划 #计数 
[494. 目标和 - 力扣（LeetCode）](https://leetcode.cn/problems/target-sum/)

>错误版
```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        # plus - minus = target
        # plus + minus = sum
        # plus = (target + sum) / 2
        # dp[j] 记录有dp[j]种方法让目标和为j
        # 
        # dp[j] = max(dp[j], dp[j - i] + 1)
        sum0 = sum(nums) + target
        if sum0 % 2 == 1:
            return 0
        sum_ = sum0 // 2
        dp = [0] * (sum_ + 1)
        for i in nums:
            for j in range(sum_, i - 1, -1):
                print("j, dp[j], dp[j - i] + 1:\n", j, dp[j], dp[j - i] + 1)
                dp[j] = max(dp[j], dp[j - i] + 1)
        return dp[sum_]
                
```

>提示通过版
```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:)
        sum0 = sum(nums) + target
        if sum0 % 2 == 1 or sum0 < 0:
            return 0
        sum_ = sum0 // 2
        dp = [0] * (sum_ + 1)
        dp[0] = 1
        for i in nums:
            for j in range(sum_, i - 1, -1):
                dp[j] = dp[j] + dp[j - i]
        return dp[sum_]
                
```

>注释版
```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        # 👉 先做数学转化：把问题变成子集和（先转化再DP）
        # plus - minus = target
        # plus + minus = sum
        # => plus = (target + sum) / 2
        
        sum0 = sum(nums) + target
        # 👉 注意合法性（不是所有情况都有解）
        if sum0 % 2 == 1 or sum0 < 0:
            return 0
        
        sum_ = sum0 // 2
        
        # 👉 dp[j] 定义：凑出和为 j 的“方法数”（先定义状态，再写转移）
        dp = [0] * (sum_ + 1)
        
        # 👉 空集合：什么都不选凑出 0，有 1 种方法（组合DP的基石）
        dp[0] = 1
        
        for i in nums:
            # 👉 倒序：避免一个元素被使用多次（0/1背包）
            for j in range(sum_, i - 1, -1):
                
                # 👉 核心转移：
                # dp[j] 原有方法 + 所有能由 j-i 转移来的方法
                # ❗这里是“方案数累加”，不是“选一个元素(+1)”
                # ❗不要写 max，这是计数问题不是最优化问题
                dp[j] = dp[j] + dp[j - i]
        
        # 👉 最终答案：凑出 sum_ 的总方法数
        return dp[sum_]
```


> 1. ❌ 把“方案数问题”误判成“最优化问题” → 👉 先判断题目是在问“多少种”还是“最优值”
> 2. ❌ 把“选一个元素(+1)”当成“增加一种方案” → 👉 “+1”是数量，“+dp[...]”才是方案传播
> 3. ❌ 忽略空集合的意义（dp[0]） → 👉 组合类 DP 必须先定义“什么都不选”的状态
> 4. ❌ 先写转移方程而没定义状态 → 👉 必须先用一句话说清 dp[j] 表示什么
> 5. ❌ 混淆两类加法逻辑 → 👉 区分“累加方案数”和“更新最优值”是两种完全不同的 DP
> 6. ❌ DP 三要素割裂思考 → 👉 状态定义、转移方程、初始化必须同时设计
> 7. ❌ 没有先抽象成子问题（子集和） → 👉 先完成数学转化，再进入 DP
> 8. ❌ 写 DP 时没有持续自问目标 → 👉 每一步都要确认“我是在求最优还是在计数”


>下一版
```python

```