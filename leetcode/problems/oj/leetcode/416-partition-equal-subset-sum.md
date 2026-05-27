#背包问题 #动态规划 #存在性
[416. 分割等和子集 - 力扣（LeetCode）](https://leetcode.cn/problems/partition-equal-subset-sum/)

>手写通过
```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        sum_nums = sum(nums)
        if sum_nums % 2 == 1:
            return False
        target = sum_nums / 2
        n = len(nums)
        target = int(target)
        dp = [0] * (target + 1)
        for i in range(n):
            for j in range(target, 0, -1):
                if j - nums[i] >= 0 and dp[j - nums[i]] + nums[i] <= j:
                    dp[j] = max(dp[j - nums[i]] + nums[i], dp[j])
        if dp[target] == target:
            return True
        else:
            return False
```

>GPT优化版
```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        sum_nums = sum(nums)
        if sum_nums % 2 == 1:
            return False

        target = sum_nums // 2  # 优化1：原来是 sum_nums / 2 再 int()，改为直接整除 //

        n = len(nums)
        dp = [0] * (target + 1)

        for i in range(n):
            for j in range(target, nums[i] - 1, -1):  # 优化2：原来是 range(target, 0, -1)，
                                                      # 现在从 nums[i] 开始，避免 j < nums[i] 的无效循环

                dp[j] = max(dp[j - nums[i]] + nums[i], dp[j])  
                # 优化3：删除原来的判断
                # if j - nums[i] >= 0 and dp[j - nums[i]] + nums[i] <= j
                # 因为 j >= nums[i] 已由循环保证，第二个条件恒成立

            if dp[target] == target:  # 优化4：提前终止，一旦装满 target 就直接返回
                return True

        return False  # 优化5：简化原来的 if-else 返回结构
```

>标准答案
```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        s = sum(nums)
        if s % 2:
            return False
        
        target = s // 2
        dp = [False] * (target + 1)
        dp[0] = True
        
        for num in nums:
            for j in range(target, num - 1, -1):
                dp[j] |= dp[j - num]
        
        return dp[target]
```

---

# 💡 背包方法论：布尔 DP vs 最大价值 DP

## 1️⃣ 核心触发条件（什么时候选哪种）

|情况|使用方法|触发条件 / 关键词|
|---|---|---|
|**判定型 / 可达性问题**|**布尔 DP**|题目只问“能否凑成目标/子集/容量”？关键字：**能否、是否、True/False、分割等和、目标和**|
|**价值优化 / 最大价值问题**|**最大价值 DP**|题目问“最大价值/最小代价/最优解”？关键字：**最大化、最小化、收益、价值、代价**|

### 🔹 判断逻辑：

1. **问题目标是 Yes/No → 布尔 DP**
    
    - 只关心“能否达到目标”
        
    - 状态 dp[j] = True / False
        
    - 循环顺序：
        
        - 01 背包 → 倒序
            
        - 完全背包 → 正序
            
2. **问题目标是最大/最小 → 最大价值 DP**
    
    - 关心“最优值”
        
    - 状态 dp[j] = 当前容量可达到的最大价值
        
    - 循环顺序：
        
        - 01 背包 → 倒序
            
        - 完全背包 → 正序
            

---

## 2️⃣ 关键词触发法

|关键词|触发方法|
|---|---|
|能否、是否、分割、目标和、子集|**布尔 DP**|
|最大、最小、价值、代价、收益|**最大价值 DP**|

> 口诀记忆：  
> “问能不能 → 布尔，问最优值 → 最大价值”

---

## 3️⃣ 深刻理解 / 模板化哲学

### 🔹 布尔 DP

- **状态本质**：子集和是否可达
    
- **模板化**：高度通用，几乎不改循环就能套用
    
- **局限**：不能求最大值/最优值
    
- **优势**：
    
    - 简洁、常数小
        
    - 极大容量可用位运算优化
        
    - 判定类问题几乎通用模板
        

### 🔹 最大价值 DP

- **状态本质**：容量 j 的最优值
    
- **模板化**：只适合 01 背包 / 完全背包 / 多重背包
    
- **优势**：能求最大价值 / 最小代价 / 最优解
    
- **局限**：判定类问题用起来稍显冗余，模板可迁移性略低
    

---

## 4️⃣ 方法选择流程（思维流程图）

1. 看题目标：
    
    - ❓ 问**能否/存在** → 布尔 DP
        
    - ❓ 问**最大/最小/最优值** → 最大价值 DP
        
2. 判断背包类型：
    
    - 01 背包 → 倒序循环
        
    - 完全背包 → 正序循环
        
    - 多重背包 → 可用“拆分物品 + 倒序循环”或其他优化
        
3. 确定状态：
    
    - 布尔 DP → dp[j] = True/False
        
    - 最大价值 DP → dp[j] = 最大价值
        
4. 是否可优化：
    
    - 布尔 DP → 位运算可节省空间
        
    - 最大价值 DP → 提前终止 / 剪枝
        

---

✅ **一句话总结**：

> “能否凑 → 布尔 DP，最大最小 → 最大价值 DP；01 背包倒序，完全背包正序，状态定义决定模板化深度。”

---


>下一版
```python

```