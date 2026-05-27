#前缀和  
[1480. 一维数组的动态和 - 力扣（LeetCode）](https://leetcode.cn/problems/running-sum-of-1d-array/)

>秒
```python
from itertools import accumulate
class Solution:
    def runningSum(self, nums: List[int]) -> List[int]:
        return list(accumulate(nums))
```