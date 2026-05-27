#差分数组 
[2848. 与车相交的点 - 力扣（LeetCode）](https://leetcode.cn/problems/points-that-intersect-with-cars/description/)

>下标晕了
```python
from itertools import accumulate

class Solution:
    def numberOfPoints(self, nums: List[List[int]]) -> int:
        n = max(list(map(lambda x: x[1], nums)))
        v = [0] * (n + 2)
        
        for l, r in nums:
            v[l] += 1
            # ❌ 错误 1：差分数组的“右边界”下车点标错了
            # 题目说区间是包含 r 的。如果你在 r 这里 -1，
            # 那么 r 这个点原本的 +1 就被抵消了，等于 r 这个点没被车覆盖。
            # 👉 正确做法：应该在 r 的后一个位置（r + 1）取消覆盖。
            v[r] -= 1  # 应该改为：v[r + 1] -= 1

        sum_ = list(accumulate(v))

        # ❌ 错误 2：统计逻辑完全错了
        # 你的逻辑是：“只要遇到第一个没有车的位置（sum_[i] == 0），就直接停止并返回前面的长度”。
        # 假设车停在 [1, 2] 和 [5, 6]，中间的 3 和 4 是空的。
        # 你的循环走到 3 发现是 0，就直接 return 2 了，导致后面的 [5, 6] 彻底被漏掉。
        # 👉 正确做法：不能 return，而是要遍历所有点，把有车覆盖的点（> 0）加起来。
        for i in range(1, n +1):
            if sum_[i] == 0:
                return i - 1 
        return n
```


>修正版
```python
from itertools import accumulate

class Solution:
    def numberOfPoints(self, nums: List[List[int]]) -> int:
        # 简化一下求最大值的写法
        n = max(x[1] for x in nums)
        
        # 为了容纳 r + 1，数组长度开 n + 2 刚刚好
        v = [0] * (n + 2)
        
        for l, r in nums:
            v[l] += 1
            v[r + 1] -= 1  # 修复 1：在 r 的后一个位置取消覆盖
            
        sum_ = list(accumulate(v))

        # 修复 2：统计所有覆盖次数大于 0 的点
        ans = 0
        for i in range(1, n + 1):
            if sum_[i] > 0:
                ans += 1
                
        return ans
```


>Gemini标准版
```python
from itertools import accumulate

class Solution:
    def numberOfPoints(self, nums: List[List[int]]) -> int:
        # 因为题目限制 starti, endi <= 100，开 102 的数组完美容纳 end + 1
        diff = [0] * 102
        
        for start, end in nums:
            diff[start] += 1
            diff[end + 1] -= 1  # 永远记住，右边界的下一位减1
            
        # 一行流：求前缀和，并统计大于 0 的点的个数
        return sum(1 for x in accumulate(diff) if x > 0)
```

>合并区间版
```python
class Solution:
    def numberOfPoints(self, nums: List[List[int]]) -> int:
        # 1. 必须先按每辆车的起点从小到大排序
        nums.sort(key=lambda x: x[0])
        
        ans = 0
        cur_end = -1 # 记录当前连续覆盖区间的极右边界
        
        for start, end in nums:
            if start > cur_end:
                # 发现断层！和前面的车不挨着，直接加上这辆车的长度
                ans += end - start + 1
                cur_end = end
            else:
                # 产生重叠！如果这辆车伸得更长，就把多出来的部分加上
                if end > cur_end:
                    ans += end - cur_end
                    cur_end = end # 更新极右边界
                    
        return ans
```