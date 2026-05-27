[合并区间_牛客题霸_牛客网](https://www.nowcoder.com/practice/69f4e5b7ad284a478777cb2a17fb5e6a)
```python
# class Interval:
#     def __init__(self, a=0, b=0):
#         self.start = a
#         self.end = b
#
# 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
#
#
# @param intervals Interval类一维数组
# @return Interval类一维数组
#
class Solution:
    def merge(self, intervals: List[Interval]) -> List[Interval]:
        # write code here
        # 显式指定排序规则：首先按 start 排序，如果 start 相同，则按 end 排序
        intervals.sort(key=lambda x: (x.start, x.end))

        # 存放合并后的区间
        merged = []

        for interval in intervals:
            # 如果 merged 为空或当前区间与 merged 中最后一个区间不重叠，直接添加
            if not merged or merged[-1].end < interval.start:
                merged.append(interval)
            else:
                # 有重叠时，更新 merged 中最后一个区间的 end 为两个区间 end 的较大者
                merged[-1].end = max(merged[-1].end, interval.end)

        return merged

```