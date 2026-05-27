#滑动窗口 [209. 长度最小的子数组 - 力扣（LeetCode）](https://leetcode.cn/problems/minimum-size-subarray-sum/description/)

```c++
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int n = nums.size();
        int r = 0;
        int ans = n;
        int sum = 0;
        for(int i=0;i<n;i++){
            while(r<n && sum < target){
                sum+=nums[r];
                r++;
            }
            if(i==0 && r==n && sum < target){
                return 0;
            }
            if(sum >= target){
                ans = min(ans, r-i);
            }
            sum-=nums[i];
        }
        return ans;
    }
};
```

>缺陷通过版
```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        n = len(nums)
        ans = float('inf')
        sum = nums[0]
        l, r = 0, 0
        while l <= r and r < n:
            if sum >= target:
                ans = min(r - l + 1, ans)
                sum -= nums[l]
                l += 1
            else:
                r += 1
                if r < n:
                    sum += nums[r]
        if ans == float('inf') and sum < target:
            return 0
        return ans
```

>gpt微调版
```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        n = len(nums)
        ans = float('inf')
        sum_ = 0   # 从0开始
        l, r = 0, 0

        while r < n:  # 只用一个while
            sum_ += nums[r]  # 先累加右边元素

            if sum_ >= target:  # 缩左指针
                ans = min(ans, r - l + 1)
                sum_ -= nums[l]
                l += 1
            else:
                r += 1  # 右移窗口

        # 最后可能 ans==inf 表示无解
        return 0 if ans == float('inf') else ans
```

>gpt标准版模板做法-可迁移性强
```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        n = len(nums)
        ans = float('inf')  # 无解判定
        window_sum = 0
        l = 0

        for r in range(n):               # 右指针扩张
            window_sum += nums[r]

            while window_sum >= target:   # 条件成立 → 缩左指针优化
                ans = min(ans, r - l + 1)
                window_sum -= nums[l]
                l += 1

        return 0 if ans == float('inf') else ans
```

>下一次做题待续
```python
```





好的，我们从 **方法论层面**来分析“最小连续子数组和 ≥ target”这类问题，给出**标准化、可迁移的模板**，并说明为什么这是通用方法，能迁移到多类题目。

---

# 一、问题本质抽象

题目：`minSubArrayLen(target, nums)`

抽象：

1. **数组** → `nums`
    
2. **窗口** → 我们要找一个连续子数组
    
3. **约束条件** → sum(窗口) ≥ target
    
4. **目标** → 窗口最短长度
    

泛化：

- 题目可以抽象为：**在数组上找最小/最大连续区间，使窗口满足某个条件**
    
- “条件”可以是：
    
    - sum ≥ target
        
    - 乘积 ≥ target
        
    - 窗口内满足最多/最少某种元素
        
- 所以可以抽象成 **滑动窗口 + 条件判断** 模板
    

---

# 二、方法论

## 1️⃣ 窗口的概念

- **左指针 l**：窗口开始
    
- **右指针 r**：窗口结束
    
- **窗口维护的值**：sum/乘积/计数/最大最小值
    

---

## 2️⃣ 窗口扩张/缩小规则

- **右指针扩张** → 增加窗口，使条件可能成立
    
- **左指针缩小** → 当条件成立时尝试优化（最小长度/最大长度）
    

> 核心思想：**动态维护满足条件的最优窗口**

---

## 3️⃣ 初始条件与边界处理

- **sum/计数初始为 0** → 避免边界陷阱
    
- **ans 初始为 ∞ 或其他极值** → 用于无解判断
    
- **循环条件** → `while r < n` 或 `for r in range(n)`
    
- **内部循环或条件** → `while 条件成立: 缩左指针`
    

---

## 4️⃣ 标准模板（Python）

```python
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        n = len(nums)
        ans = float('inf')  # 无解判定
        window_sum = 0
        l = 0

        for r in range(n):               # 右指针扩张
            window_sum += nums[r]

            while window_sum >= target:   # 条件成立 → 缩左指针优化
                ans = min(ans, r - l + 1)
                window_sum -= nums[l]
                l += 1

        return 0 if ans == float('inf') else ans
```

---

# 三、为什么这是通用方法

1. **抽象能力**：
    

- “最小连续子数组和 ≥ target”
    
- 可以迁移到 **最大连续子数组和 ≤ target**
    
- 可以迁移到 **长度最短/最长子串问题**
    
- 可以迁移到 **窗口内元素数量/种类约束问题**
    

2. **核心原则**：
    

- **条件成立 → 缩左指针** → 尝试最优
    
- **条件不成立 → 扩右指针** → 尝试满足条件
    

无论条件是什么，滑动窗口方法都成立。

---

# 四、可迁移性的体现

|题目类型|滑动窗口方法迁移|
|---|---|
|最小连续子数组和 ≥ target|当前题目|
|最大连续子数组和 ≤ target|右扩加，左缩减保证条件|
|最长不重复子串|用 set 维护窗口内元素，条件：没有重复|
|最多 K 个不同字符|用字典统计字符数量，条件：len(dict) ≤ K|
|最长连续 1|条件：窗口内 0 个数 ≤ 0 或 ≤ K|

> 核心迁移点：**窗口动态维护 + 条件判断**

---

# 五、总结方法论

1. **模式识别** → “最小/最大连续子数组/子串问题”
    
2. **抽象窗口** → 左右指针 + 窗口值
    
3. **维护条件** → 根据题目定义
    
4. **更新最优解** → 满足条件时尝试优化窗口
    
5. **边界处理** → 初始值、无解情况
    

---

✅ **方法论核心口诀**：

```text
右扩寻找条件成立
左缩优化目标值
ans初始化无穷大
边界判定最后做
```

> 用这个套路，你几乎能解掉所有**最小/最大连续窗口问题**，这是“可迁移性”的体现。

---
