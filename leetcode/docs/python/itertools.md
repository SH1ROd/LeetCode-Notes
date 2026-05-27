既然你想一次性掌握这个“算法外挂”库，那我们就来个大全套！

在刷题（如 LeetCode）时，`itertools` 中大约有十几把“尖刀”是最常用的。为了方便记忆，我将它们分为四大类：**排列组合、序列拼接与拆分、条件过滤、以及无限迭代与辅助**。

这里是为你整理的 `itertools` 算法题实战全家桶：

---

### 一、 排列组合类（回溯、暴力枚举克星）

这类函数主要用于在一维数组中寻找所有可能的结果，经常能把几十行的回溯代码缩减成一行。

- **`combinations(iterable, r)`**：**无放回组合**。选出 `r` 个元素，不考虑顺序。
    
- **`permutations(iterable, r=None)`**：**无放回排列**。选出 `r` 个元素，考虑顺序。
    
- **`combinations_with_replacement(iterable, r)`**：**有放回组合**。选出 `r` 个元素，元素可以重复被选中。（在类似“零钱兑换”的暴力枚举中很有用）。
    
    Python
    
    ```
    from itertools import combinations_with_replacement
    list(combinations_with_replacement([1, 2], 2))
    # 输出: [(1, 1), (1, 2), (2, 2)]
    ```
    
- **`product(*iterables, repeat=1)`**：**笛卡尔积**。相当于多层嵌套 `for` 循环。
    
    Python
    
    ```
    from itertools import product
    # 求一个数组自身与自身的组合（常用于二维矩阵坐标遍历）
    list(product([0, 1], repeat=2)) 
    # 输出: [(0, 0), (0, 1), (1, 0), (1, 1)]
    ```
    

### 二、 序列操作类（扁平化、双指针辅助）

在处理多维数组、不等长数组或相邻元素时，这些函数能大幅减少越界报错的风险。

- **`chain(*iterables)`**：**多数组拼接**。
    
- **`chain.from_iterable(iterable)`**：**二维数组降维打击（扁平化）**。这是极高频的技巧！
    
    Python
    
    ```
    from itertools import chain
    matrix = [[1, 2], [3, 4], [5]]
    list(chain.from_iterable(matrix))
    # 输出: [1, 2, 3, 4, 5]
    ```
    
- **`zip_longest(*iterables, fillvalue=None)`**：**不等长数组的 zip**。普通的 `zip` 会在最短的数组结束时停止，而 `zip_longest` 会以最长的为准，缺失的部分用 `fillvalue` 填充。（在处理“大数相加”或“合并两个不等长链表”的逻辑时有奇效）。
    
    Python
    
    ```
    from itertools import zip_longest
    list(zip_longest('AB', '123', fillvalue='0'))
    # 输出: [('A', '1'), ('B', '2'), ('0', '3')]
    ```
    
- **`pairwise(iterable)`**：**相邻元素滑动窗口**（Python 3.10+）。每次返回 `(当前元素, 下一个元素)`。
    

### 三、 状态聚合与计算类

用于对数组进行连续状态的统计或预处理。
- **[[accumulate]]**：**前缀状态机**。默认求前缀和，但通过传入自定义函数，可以求”前缀最大值”、”前缀乘积”等。
    
    Python
    
    ```
    from itertools import accumulate
    # 求前缀最大值
    list(accumulate([3, 1, 4, 1, 5], max))
    # 输出: [3, 3, 4, 4, 5]
    ```
    
- **`groupby(iterable, key=None)`**：**连续相同元素分组**。常用于“游程编码”（Run-Length Encoding）或压缩字符串。
    

### 四、 高级切片与过滤类

当你需要对迭代器（不能直接用 `[start:end]` 切片的对象）进行操作时。

- **`islice(iterable, start, stop, step)`**：**迭代器切片**。当你用生成器生成了大量数据，只想取其中一段时，用它不会把所有数据加载进内存。
    
    Python
    
    ```
    from itertools import islice
    # 获取迭代器的前3个元素
    list(islice((x**2 for x in range(100)), 3))
    # 输出: [0, 1, 4]
    ```
    
- **`compress(data, selectors)`**：**掩码过滤**。根据一个布尔数组来筛选数据。（结合二进制位运算求子集时非常好用）。
    
    Python
    
    ```
    from itertools import compress
    list(compress(['A', 'B', 'C'], [1, 0, 1]))
    # 输出: ['A', 'C']
    ```
    

### 五、 无限迭代器（高阶辅助）

这些函数会无限生成数据，通常配合 `zip` 或 `break` 使用。

- **`count(start=0, step=1)`**：**无限计数器**。在优先队列（Heap）中极其有用！如果两个任务优先级相同，堆会比较下一个元素。插入 `count()` 可以作为稳定排序的 tie-breaker（打破平局的标志）。
    
    Python
    
    ```
    import heapq
    from itertools import count
    
    counter = count()
    pq = []
    # (优先级, 插入顺序, 任务名)
    heapq.heappush(pq, (1, next(counter), 'task A'))
    heapq.heappush(pq, (1, next(counter), 'task B'))
    ```
    
- **`cycle(iterable)`**：**无限循环数组**。常用于模拟环形数组（如“击鼓传花”、“轮转数组”）。
    
- **`repeat(object, times=None)`**：**重复生成同一个值**。
    

---

把这份清单当成你的“武器库”，以后遇到需要写丑陋的多层嵌套循环、或者繁琐的边界条件处理时，想一想是不是可以用其中的某个函数一行解决。

**接下来，你想找一道具体的算法题（比如需要降维、或者大数合并的题目），来亲手测试一下这些方法的实战手感吗？**