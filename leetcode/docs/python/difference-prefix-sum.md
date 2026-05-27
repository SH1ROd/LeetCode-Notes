
### 🚀 差分 + 前缀和 综合模板 (Python)

Python

```python
from itertools import accumulate

# n: 数组长度, m: 操作次数
n, m = map(int, input().split())

# 1. 原始数组 (假设下标从 0 开始，方便 accumulate 处理)
# 如果初始数组全是 0，直接 a = [0] * n
a = list(map(int, input().split()))

# 2. 构建初始差分数组 d
# d[0] = a[0], d[i] = a[i] - a[i-1]
d = [a[0]] + [a[i] - a[i-1] for i in range(1, n)]
d.append(0) # 多开一位，防止 r+1 越界

# 3. 执行 m 次区间修改 [l, r] 增加 c (这里假设 l, r 是 0-indexed)
for _ in range(m):
    l, r, c = map(int, input().split())
    d[l] += c
    if r + 1 < n:
        d[r + 1] -= c

# 4. 使用 accumulate 计算前缀和，一键还原回原数组
# accumulate(d) 得到的就是修改后的 a[0], a[1], ..., a[n-1]
result = list(accumulate(d[:n]))

print(*result)
```

---

### 📝 核心知识点梳理

#### 1. 前缀和模板 (单纯求区间和)

如果你只是想快速求一个静态数组的区间和，直接用 `accumulate` 预处理：

Python

```python
from itertools import accumulate

arr = [1, 2, 3, 4, 5]
# 得到 [0, 1, 3, 6, 10, 15] (前面补个0方便计算区间)
s = [0] + list(accumulate(arr))

# 求区间 [l, r] 的和 (下标从 0 开始)
# sum = s[r + 1] - s[l]
```

#### 2. 差分与前缀和的关系

- **差分数组的前缀和 = 原数组**。
    
- **原数组的差分 = 差分数组**。
    
- **区间修改 $\rightarrow$ 差分操作**：$O(1)$ 复杂度。
    
- **单点查询 $\rightarrow$ 前缀和还原**：$O(n)$ 复杂度。
    

#### 3. 为什么用 `accumulate`？

- **简洁**：省去了手动写 `for i in range: a[i] += a[i-1]` 的逻辑。
    
- **高效**：它是 C 语言实现的内置迭代器，在处理大数据量时比手写循环更快。
    

这个模板涵盖了从原数组转化、区间修改到最终还原的全过程。如果需要**二维差分**（矩阵修改）或者其他变体，随时告诉我！