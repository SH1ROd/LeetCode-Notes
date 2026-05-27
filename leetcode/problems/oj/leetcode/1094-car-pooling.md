#差分数组 
[1094. 拼车 - 力扣（LeetCode）](https://leetcode.cn/problems/car-pooling/)

>手写版
```python
from itertools import accumulate
class Solution:
    def carPooling(self, trips: List[List[int]], capacity: int) -> bool:
        n = max(x[2] for x in trips)
        diff = [0] *(n + 2)
        for t, l, r in trips:
            diff[l] += t
            diff[r] -= t
        res = accumulate(diff)
        return max(res) <= capacity
```

>Gemini
```python
from itertools import accumulate
from typing import List

class Solution:
    def carPooling(self, trips: List[List[int]], capacity: int) -> bool:
        # 直接根据题目的最大范围 1000 初始化，省去一次找 max 的时间
        diff = [0] * 1001 
        
        for t, l, r in trips:
            diff[l] += t
            diff[r] -= t
            
        # 只要历史最高载客量不超过容量即可
        return max(accumulate(diff)) <= capacity
```

>下一版
```python

```