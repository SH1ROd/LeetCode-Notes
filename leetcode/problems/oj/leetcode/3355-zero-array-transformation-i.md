#差分数组 
[3355. 零数组变换 I - 力扣（LeetCode）](https://leetcode.cn/problems/zero-array-transformation-i/description/)

>手写版
```python
from itertools import accumulate
class Solution:
    def isZeroArray(self, nums: List[int], queries: List[List[int]]) -> bool:
        n = len(nums)
        nums = [0] + nums
        diff = [0] * (n + 2)
        for i in range(1, n + 1):
            diff[i] = nums[i] - nums[i - 1]
        print(diff)
        for l, r in queries:
            l = l + 1
            r = r + 1
            diff[l] -= 1
            diff[r + 1] += 1
        print(diff)
        ans = list(accumulate(diff))
        for i in ans[1: -1]:
            if i > 0:
                return False
        return True
```


>下一版
```python

```


>Gemini版
```python
from itertools import accumulate
from typing import List

class Solution:
    def isZeroArray(self, nums: List[int], queries: List[List[int]]) -> bool:
        n = len(nums)
        if n == 0:
            return True
            
        # 长度只需要 n + 1，最后一位留给 r + 1
        diff = [0] * (n + 1)
        
        # 1. 把 nums 转化为差分数组（原汁原味的 0 索引）
        diff[0] = nums[0]  # 单独处理第 0 位，避免 i-1 越界
        for i in range(1, n):
            diff[i] = nums[i] - nums[i - 1]
            
        # 2. 合并 queries 的修改，直接用原下标！
        for l, r in queries:
            diff[l] -= 1
            diff[r + 1] += 1
            
        # 3. 还原数组
        ans = list(accumulate(diff))
        
        # 4. 检查前 n 个元素即可
        for i in range(n):
            if ans[i] > 0:
                return False
                
        return True
```

总结差分数组的 0 索引写法，我为你编了一个简单顺口的四句七字口诀，专门针对你觉得“怪怪的”那些下标痛点：

### 🌟 差分数组 0 索引口诀：

> **差分长度要加一，**
> 
> **首位不变后减前。**
> 
> **左标原位右加一，**
> 
> **前缀求和只看 N。**

---

### 📖 口诀拆解对应代码：

**1. 差分长度要加一**

- **代码**：`diff = [0] * (n + 1)`
    
- **含义**：永远记得给差分数组多留 1 个位置，这是为了包容区间操作时 `r + 1` 不越界。
    

**2. 首位不变后减前**

- **代码**：`diff[0] = nums[0]`，然后 `diff[i] = nums[i] - nums[i - 1]`
    
- **含义**：原数组不用前面补 0。第 0 位直接照抄原数组，后面的正常用当前项减去前一项。
    

**3. 左标原位右加一**

- **代码**：`diff[l] -= 1`，`diff[r + 1] += 1`
    
- **含义**：处理 `[l, r]` 区间时，左边界 `l` 是多少就填多少，**只有右边界 `r` 需要加 1**（符号相反）。
    

**4. 前缀求和只看 N**

- **代码**：`ans = list(accumulate(diff))`，遍历 `range(n)`
    
- **含义**：最后用前缀和还原时，出来的数组长度是 `n + 1`。但我们根本不用管最后一个数，直接遍历前 `n` 个数（正好对应原数组的 `0` 到 `n-1`），就完全不会切错片了。
    

有了这个口诀，下次再写差分数组，只要心里默念这四句，下标绝对指哪打哪，再也不会被 `+1` 还是 `-1` 绕晕了！