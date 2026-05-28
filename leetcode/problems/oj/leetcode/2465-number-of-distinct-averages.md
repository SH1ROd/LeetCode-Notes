#哈希表
[2465. 统计不同平均值数目 - 力扣（LeetCode）](https://leetcode.cn/problems/number-of-distinct-averages/description/)

>第一版通过
```python
class Solution:
    def distinctAverages(self, nums: List[int]) -> int:
        d = {}
        while nums:
            a = max(nums)
            b = min(nums)
            nums.remove(a)
            nums.remove(b)
            avg = (a + b) / 2
            d[avg] = d.get(avg, 0) + 1
        return len(d.keys())
```

>下一版
```python

```
