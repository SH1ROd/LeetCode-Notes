
>提示词： 
>
>为什么我一直做不对，我的思路有什么问题, 分析我的每一版之间的我的脑袋思考变化，我在想什么，应该怎么纠正
>
>帮我之前错误的几版和现在和这个通过版都写一下注释，标注你上面的观点
>
>这题我也止步于此了，我的想法不对吗，我的思维有什么缺陷，为什么还是没法想到，缺少方法论吗，我拿到这题看不出口诀或者模板：


> 使用方式：  
> 刷题 → 没思路 → 打开手册 → 根据关键词匹配算法模型

---

# 一、最重要的8句口诀（先记住）

```
连续递推看前一
区间限制滑动窗
子数组和前缀和
最优问题多DP
所有组合用回溯
最短路径用BFS
下个更大单调栈
有序查找用二分
```

如果只记住这一段，你已经能判断 **60% 的题型**。

---

# 二、算法模型速查表

|题目关键词|常见算法|
|---|---|
|连续递增 / 连续1|状态变量|
|最长子串 / 最多K个|滑动窗口|
|子数组和|前缀和|
|最大 / 最小 / 最优|动态规划|
|所有组合|回溯|
|最少步骤|BFS|
|连通区域|DFS|
|下一个更大元素|单调栈|
|有序查找|二分|

---

# 三、数组问题判断流程

做数组题时按这个顺序问自己：

```
数组问题
│
├─ 只和相邻元素有关？
│     → 状态变量
│
├─ 需要维护一个区间？
│     → 滑动窗口
│
├─ 求区间和？
│     → 前缀和
│
└─ 求最优解？
      → 动态规划
```

---

# 四、算法模型详解

---

# 1 连续状态模型

### 关键词

```
连续
递增
递减
连续1
```

### 思路

只依赖前一个元素。

### 模板

```python
cur = 1
ans = 1

for i in range(1,n):
    if nums[i] > nums[i-1]:
        cur += 1
    else:
        cur = 1
        
    ans = max(ans,cur)
```

### 典型题

- Longest Continuous Increasing Subsequence
    
- Max Consecutive Ones
    

复杂度：

```
O(n)
```

---

# 2 滑动窗口

### 关键词

```
最长子串
最多K个
不重复字符
窗口
```

### 思路

维护一个合法区间 `[l,r]`

### 模板

```python
l = 0

for r in range(n):

    add(nums[r])

    while 窗口不合法:
        remove(nums[l])
        l += 1

    更新答案
```

### 典型题

- Longest Substring Without Repeating Characters
    
- Minimum Window Substring
    
- Longest Repeating Character Replacement
    

复杂度

```
O(n)
```

---

# 3 前缀和

### 关键词

```
subarray sum
区间和
和为K
```

### 核心公式

```
sum(l,r) = prefix[r] - prefix[l]
```

### 模板

```python
prefix = 0
hashmap = {0:1}

for num in nums:

    prefix += num

    if prefix-k in hashmap:
        ans += hashmap[prefix-k]

    hashmap[prefix] += 1
```

### 典型题

- Subarray Sum Equals K
    

---

# 4 动态规划 DP

### 关键词

```
最大
最小
最优
多少种
方案数
```

### 思路

当前状态由之前状态转移。

### 模板

```
dp[i] = f(dp[i-1], dp[i-2], ...)
```

### 例子

```python
dp[i] = max(
    dp[i-1],
    dp[i-2] + nums[i]
)
```

### 典型题

- House Robber
    
- Climbing Stairs
    
- Maximum Subarray
    

---

# 5 回溯

### 关键词

```
所有组合
所有排列
所有可能
```

### 思路

枚举所有路径。

### 模板

```python
def backtrack(path):

    if 满足条件:
        res.append(path)
        return

    for choice in choices:

        path.append(choice)

        backtrack(path)

        path.pop()
```

### 典型题

- Permutations
    
- Subsets
    
- Combinations
    

---

# 6 二分查找

### 关键词

```
有序
查找
最小满足条件
```

### 模板

```python
l = 0
r = n

while l < r:

    mid = (l+r)//2

    if condition(mid):
        r = mid
    else:
        l = mid + 1
```

复杂度

```
O(log n)
```

---

# 7 单调栈

### 关键词

```
下一个更大元素
温度
柱状图面积
```

### 思路

维护单调递增 / 递减栈。

### 模板

```python
stack = []

for i in range(n):

    while stack and nums[i] > nums[stack[-1]]:
        stack.pop()

    stack.append(i)
```

### 典型题

- Daily Temperatures
    
- Next Greater Element
    

---

# 8 BFS

### 关键词

```
最少步骤
最短路径
层级
```

### 模板

```python
from collections import deque

queue = deque([start])

while queue:

    node = queue.popleft()

    for nxt in neighbors:

        queue.append(nxt)
```

---

# 9 DFS

### 关键词

```
岛屿
连通区域
遍历
```

### 模板

```python
def dfs(x,y):

    if 越界:
        return

    dfs(x+1,y)
    dfs(x-1,y)
    dfs(x,y+1)
    dfs(x,y-1)
```

### 典型题

- Number of Islands
    

---

# 10 树递归

### 关键词

```
二叉树
深度
路径
祖先
```

### 模板

```python
def dfs(node):

    if not node:
        return

    left = dfs(node.left)
    right = dfs(node.right)
```

---

# 五、推荐刷题顺序

建议按难度逐步学习：

```
1 数组基础
2 双指针
3 滑动窗口
4 前缀和
5 二分查找
6 栈 / 单调栈
7 DFS / BFS
8 动态规划
9 回溯
10 树
```

---

# 六、刷题建议

正确学习流程：

```
刷题
↓
不会
↓
查算法模型
↓
学算法
↓
再刷类似题
```

而不是：

```
先学所有算法
再刷题
```

那样几乎没人能坚持。

---

# 七、给自己的补充区

以后刷题可以自己补充：

```
题目：
算法模型：
关键思路：
代码模板：
```

这样这份手册会越来越强。