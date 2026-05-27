#双指针 
[674. 最长连续递增序列 - 力扣（LeetCode）](https://leetcode.cn/problems/longest-continuous-increasing-subsequence/description/)
```python
if not nums:  # 处理空数组的情况
            return 0
        
        # 初始化
        l = 0
        ans = 1  # 至少有一个元素是递增序列
        
        # 遍历数组
        for r in range(1, len(nums)):
            # 如果当前元素大于前一个元素，说明递增序列继续
            if nums[r] > nums[r - 1]:
                # 更新答案
                ans = max(ans, r - l + 1)
            else:
                # 如果不递增，则更新 l 为当前的 r
                l = r
        
        return ans
```

>半小时版本
```python
class Solution:
    def findLengthOfLCIS(self, nums: List[int]) -> int:
        ans = 1
        n = len(nums)
        l, r = 0, 1
        while(r < n):
            if nums[r] <= nums[r - 1]:
                ans = max (ans, r - l)
                l = r
            r += 1
        ans = max (ans, r - l)
        return ans
```

>gpt版本
```python
cur = 1
ans = 1

for i in range(1, len(nums)):
    if nums[i] > nums[i-1]:
        cur += 1
    else:
        cur = 1
    ans = max(ans, cur)

return ans
```

>总结方法：
>	1 相邻关系？
>	2 区间关系？
>	3 前缀关系？
>	4 最优结构？
>对应:
>	1 状态变量
>	2 滑动窗口
>	3 前缀和
>	4 DP