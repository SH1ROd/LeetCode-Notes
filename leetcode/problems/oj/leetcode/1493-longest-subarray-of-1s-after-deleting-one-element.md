#滑动窗口 
[1493. 删掉一个元素以后全为 1 的最长子数组 - 力扣（LeetCode）](https://leetcode.cn/problems/longest-subarray-of-1s-after-deleting-one-element/description/?envType=problem-list-v2&envId=sliding-window&)

>失败的思路
```python
class Solution:
    def longestSubarray(self, nums: List[int]) -> int:
        # n * (n - 1区间找最长1子串)
        # dp[i]记录0-i这个子串，删掉一个元素后最长1子串的长度
        # 维护(n - 1区间最长子串长度)
        # i * (0到i的区间去除一个元素，找最长1子串)
        # 最长子串的非首尾元素会有一个不是1的元素，如果在首或尾，那就没必要长度就变了原长-1
        # 要记录这个数据有没有使用非1元素，0次或1次-二维dp？
        # dp[i][1] = dp[i -1][1] + 1 如果最长子串末尾就是i-1，且使用非1元素，且nums[i]=1
        # dp[i][1] = dp[i -1][1]     如果最长子串末尾就是i-1，且使用非1元素，且nums[i]!=1
        # dp[i][1] = dp[i -1][1]     如果最长子串末尾不是i-1，且使用非1元素
        
        # dp[i][0] = dp[i -1][0] + 1 如果最长子串末尾就是i-1，且没非1元素，且nums[i]=1
        # dp[i][1] = dp[i -1][0] + 1 如果最长子串末尾就是i-1，且没非1元素，且nums[i]!=1
        # dp[i][1] = dp[i -1][0] + 1  如果最长子串末尾就是i-2，且没非1元素,且nums[i]=1，且nums[i-1]=0
        # dp[i][0] = dp[i -1][0]     如果最长子串末尾就是i-2，且没非1元素,且nums[i]!=1
        # p[i][j]记录最长子串末尾位置,j是有没有删除元素,dp[i][j]记录最长子串长度
        # 复杂度是n*2，但是条件好复杂
        n = len(nums)
        dp[[0] *2] * (n + 1)
        for i in range(1, n + 1):
            for j in range(2):
                if j = 0:
                    dp[i][j]
```

>第一版
```python
class Solution:
    def longestSubarray(self, nums: List[int]) -> int:
        n = len(nums)
        l = 0
        crr0 = 0
        ans = -1
        f1 = True
        for r in range(n):
            
            if nums[r] == 0:
                f1 = False
                crr0 += 1
            while crr0 > 1:
                if nums[l] == 0:
                    crr0 -= 1
                l += 1
            ans = max(ans, r - l)
        if f1:
            return n - 1
        else:
            return ans
```

>GPT版
```python
class Solution:
    def longestSubarray(self, nums: List[int]) -> int:
        n = len(nums)
        l = 0
        zeros = 0
        ans = 0
        
        for r in range(n):
            if nums[r] == 0:
                zeros += 1
            while zeros > 1:
                if nums[l] == 0:
                    zeros -= 1
                l += 1
            ans = max(ans, r - l)  # r - l 正好表示删除一个0后的长度
        
        return ans
```