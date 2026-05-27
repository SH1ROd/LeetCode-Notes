#前缀和 
[724. 寻找数组的中心下标 - 力扣（LeetCode）](https://leetcode.cn/problems/find-pivot-index/)

>下标比较容易想乱
```python
from itertools import accumulate
class Solution:
    def pivotIndex(self, nums: List[int]) -> int:
        l_sum = [0] + list(accumulate(nums)) + [0]
        r_sum = [0] + list(accumulate(nums[::-1]))[::-1] + [0]
        n = len(nums)
        for i in range(n):
            l = l_sum[i + 1 - 1] - l_sum[0]
            r = r_sum[i + 1 + 1] - r_sum[n + 1]
            if l == r:
                return i
        return -1

```

Gemini版本:
```python
from itertools import accumulate

class Solution:
    def pivotIndex(self, nums: List[int]) -> int:
        # 只在开头加 0 即可，l_sum[i] 就是 nums[i] 左侧的和
        l_sum = [0] + list(accumulate(nums))
        
        # 逆序求后缀和，再逆序回来，并在末尾加 0
        r_sum = list(accumulate(nums[::-1]))[::-1] + [0]
        
        for i in range(len(nums)):
            # 直接通过索引取值，极其清爽
            if l_sum[i] == r_sum[i + 1]:
                return i
        return -1
```