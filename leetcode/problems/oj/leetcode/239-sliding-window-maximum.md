#滑动窗口 
[239. 滑动窗口最大值 - 力扣（LeetCode）](https://leetcode.cn/problems/sliding-window-maximum/)

>拼多多面试不知道怎么做能整体做到o(n)
```python
l = -1
r = k - 2
while r < n:
	l += 1
	r += 1
	cur_max = max(nums[l: r + 1]) # 这里不知道怎么优化成维护一个队列能保证他是有序的，然后每次把nums[r]加入, nums[i - 1]剔·除, 完全没有思路，只有set能做到，但是set怎么保持有序呢？如果用大顶堆的话，好像也做不到o(1)插入和查找有开销所以没思路了
	ans.append(cur_amx)
return ans
```

>下一版
```pyhton

```