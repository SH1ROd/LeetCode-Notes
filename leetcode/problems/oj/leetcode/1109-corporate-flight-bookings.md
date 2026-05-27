#差分数组 
[1109. 航班预订统计 - 力扣（LeetCode）](https://leetcode.cn/problems/corporate-flight-bookings/description/)

>手写版
```python
from itertools import accumulate
class Solution:
    def corpFlightBookings(self, bookings: List[List[int]], n: int) -> List[int]:
        # n = max(x[1] for x in bookings)
        print(n)
        diff = [0] * (n + 1)
        for l, r, t in bookings:
            diff[l - 1] += t
            diff[min(r, n)] -= t
        ans = list(accumulate(diff))
        return ans[:-1]
```

>手写版
```python

```

>下一版
```python

```