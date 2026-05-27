#前缀和 
[303. 区域和检索 - 数组不可变 - 力扣（LeetCode）](https://leetcode.cn/problems/range-sum-query-immutable/)

>勉强过，下标有点丑
```python
class NumArray:

    def __init__(self, nums: List[int]):
        self.n = len(nums)
        self.v = [0] * (self.n + 1)
        self.v[1] = nums[0]
        for i in range(2, self.n + 1):
            self.v[i] = self.v[i - 1] + nums[i - 1]

        

    def sumRange(self, left: int, right: int) -> int:
        return self.v[right + 1] - self.v[left]


# Your NumArray object will be instantiated and called as such:
# obj = NumArray(nums)
# param_1 = obj.sumRange(left,right)
```

>Gemini： accumulate计算nums数组的前缀和，然后前面补一个[0]
```python
from itertools import accumulate

class NumArray:
    def __init__(self, nums: List[int]):
        # accumulate 自动计算前缀和，前面拼接一个 [0] 处理边界
        self.v = [0] + list(accumulate(nums))

    def sumRange(self, left: int, right: int) -> int:
        return self.v[right + 1] - self.v[left]
```