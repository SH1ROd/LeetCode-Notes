#哈希表
[3194. 最小元素和最大元素的平均值 - 力扣（LeetCode）](https://leetcode.cn/problems/minimum-average-of-smallest-and-largest-elements/description/)

>第一版通过
```python
class Solution:
    def minimumAverage(self, nums: List[int]) -> float:
        n = len(nums)
        avgs = []
        for i in range(n // 2):
            a = max(nums)
            b = min(nums)
            nums.remove(a)
            nums.remove(b)
            avgs.append((a + b) / 2)
        return min(avgs)
```

>下一版
```python

```
