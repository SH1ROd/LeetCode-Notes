
# 🎯 二分算法核心模板汇总 (Python)

## 1. 🔍 二分查找：调用标准库 (处理有序数组)

对于已经在内存中的有序列表，直接使用 `bisect` 模块。它是 C 语言实现的，性能最优。

Python

```python
import bisect

nums = [1, 2, 4, 4, 4, 6, 8]
target = 4

# 1. 找第一个 >= target 的索引 (左边界)
# 如果 target 不在数组中，返回它应该插入的位置
idx_l = bisect.bisect_left(nums, target) 

# 2. 找第一个 > target 的索引 (右边界)
idx_r = bisect.bisect_right(nums, target)

# 3. 统计 target 出现的次数
count = idx_r - idx_l

# 4. 检查 target 是否真的在数组中存在
exists = idx_l < len(nums) and nums[idx_l] == target
```

---

## 2. 🛠️ 二分答案：通用稳健模板 (逻辑判断)

这是解决“最大化最小值”或“最小化最大值”问题的标准写法。使用 `ans` 变量记录结果，逻辑最清晰，永不死循环。

Python

```python
def check(x):
    # 核心业务逻辑：判断 x 是否合法，返回 True 或 False
    pass

l, r = 0, 10**14  # 设定逻辑上下界
ans = -1

while l <= r:
    # mid = l + (r - l) // 2 防溢出
    mid = (l + r) // 2
    if check(mid):
        ans = mid      # 记录当前可行解
        # --- 情况 A: 找“最小”可行解 (如：最小化最大值) ---
        r = mid - 1    # 继续往左找更小的
        
        # --- 情况 B: 找“最大”可行解 (如：最大化最小值) ---
        # l = mid + 1  # 继续往右找更大的
    else:
        # 当前 mid 不行，往反方向找
        l = mid + 1    # 若找最小可行解，不行就往大找
        # r = mid - 1  # 若找最大可行解，不行就往小找

# 最终 ans 即为所求结果
```

---

## 3. 🧙‍♂️ 二分答案：黑魔法版 (利用库加速)

通过伪装成数组对象，利用 `bisect_left` 的底层 C 语言循环来执行 `check` 判断。适用于追求极致简洁或卡常数的场景。

Python

```python
from bisect import bisect_left

# 假设我们要找第一个满足 check(x) 为 True 的最小整数 x
# 注意：要求 check(x) 随 x 增大具有单调性 (F, F, F, T, T, T)

class Solution:
    def solve(self):
        # 内部类：模拟数组访问
        class Checker:
            def __getitem__(self, x):
                return check(x)  # 将索引访问映射为逻辑判断

        # 搜索范围 [lo, hi)
        # 寻找第一个返回 True 的位置
        ans = bisect_left(Checker(), True, lo=0, hi=10**14)
        return ans
```

---

### 💡 核心对比总结

|**场景**|**推荐工具**|**关键点**|
|---|---|---|
|**在有序 List 中找数**|`bisect_left/right`|简单、极速、无 Bug。|
|**求满足条件的“最大/最小”值**|**通用二分答案模板**|用 `ans` 变量中转，`l <= r` 配合 `+/- 1`。|
|**极致性能/代码量**|**黑魔法版 (Checker)**|仅适用于找“最小可行解”（F->T 型单调）。|