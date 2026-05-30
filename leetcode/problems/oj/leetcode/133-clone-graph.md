#哈希表 #图
[133. 克隆图 - 力扣（LeetCode）](https://leetcode.cn/problems/clone-graph/description/)

>报错版 — Optional.copy() 不存在，Python 没这个方法
```python
class Solution:
    def cloneGraph(self, node: Optional['Node']) -> Optional['Node']:
        return Optional.copy(node)  # ❌ Optional 没有 copy 方法
```

>第一版wrong — deepcopy 能过但不是考点
```python
from typing import Optional
class Solution:
    def cloneGraph(self, node: Optional['Node']) -> Optional['Node']:
        return copy.deepcopy(node)
```

>第二版wrong — 迭代硬写 neighbors[0/1]，set 不知道返回哪个新节点
```python
# ❌ 问题1: set 只能判断"见过"，但拿不到对应的新节点去连邻居
# ❌ 问题2: neighbors 是列表，不是固定 2 个元素，不能写死 0/1
# ❌ 问题3: 图可能有多个邻居，这个迭代结构扩展不了
class Solution:
    def cloneGraph(self, node: Optional['Node']) -> Optional['Node']:
        if not node or not node.neighbors:
            return node
        s = set()
        tmp = Node(node.val, [None, None])
        first = tmp
        while node not in s:
            s.add(node)
            new = Node(node.val, [tmp, None])
            tmp.neighbors[1] = new
            tmp = new
            if node.neighbors[0] not in s:
                node = node.neighbors[0]
            elif node.neighbors[1] not in s:
                node = node.neighbors[1]
            else:
                new.neighbors[1] = first
                first.neighbors[0] = new
        return first
```

>第三版wrong — 用了 dict 但存的是 node.val，node 本身没存
```python
# ❌ 问题1: 还是 neighbors[0]/[1] 硬编码
# ❌ 问题2: d 存 d[node.val] = node，应该存 d[node] = 新节点
# ❌ 问题3: s 变量未定义
class Solution:
    def cloneGraph(self, node: Optional['Node']) -> Optional['Node']:
        if not node or not node.neighbors:
            return node
        d = {}
        tmp = Node(node.val, [])
        first = tmp
        while node not in d.values():
            d[node.val] = node
            new = Node(node.val, [tmp])
            tmp.neighbors.append(new)
            tmp = new
            if node.neighbors[0] not in s:
                node = node.neighbors[0]
            elif node.neighbors[1] not in s:
                node = node.neighbors[1]
            else:
                new.neighbors[1] = first
                first.neighbors[0] = new
        return first
```

>第四版wrong — DFS 递归思路对了，else 缺 return
```python
# ✅ 思路正确：dict 存旧→新映射，DFS 递归
# ❌ 问题: else 块创建了新节点、连了邻居，但没 return
class Solution:
    def cloneGraph(self, node: Optional['Node']) -> Optional['Node']:
        d = {}
        return self.dfs(node, d)
    def dfs(self, node: Optional['Node'], d: dict):
        if node in d:
            return d[node]
        else:
            d[node] = Node(val=node.val)
            for nei in node.neighbors:
                d[node].neighbors.append(self.dfs(nei, d))
            # ❌ 缺少 return d[node]
```

>第五版wrong — 入口条件多限制了单节点情况
```python
# ✅ dfs 核心逻辑全对，return 也加了
# ❌ 问题: if not node or not node.neighbors: return node
#   单节点图没有邻居，但应该返回克隆而非原对象
class Solution:
    def cloneGraph(self, node: Optional['Node']) -> Optional['Node']:
        if not node or not node.neighbors:
            return node
        d = {}
        return self.dfs(node, d)
    def dfs(self, node: Optional['Node'], d: dict):
        if node in d:
            return d[node]
        else:
            d[node] = Node(val=node.val)
            for nei in node.neighbors:
                d[node].neighbors.append(self.dfs(nei, d))
            return d[node]
```

>最终通过
```python
from typing import Optional
class Solution:
    def cloneGraph(self, node: Optional['Node']) -> Optional['Node']:
        if not node:
            return node
        d = {}
        return self.dfs(node, d)

    def dfs(self, node: Optional['Node'], d: dict):
        if node in d:
            return d[node]
        else:
            d[node] = Node(val=node.val)
            for nei in node.neighbors:
                d[node].neighbors.append(self.dfs(nei, d))
            return d[node]
```

## 🧠 个人迁移卡

### ❌ 我卡在哪
- 浅拷贝/深拷贝概念模糊，以为这题只是在考 deepcopy
- 没理解输入是 Node 对象而非邻接表，不能用"新建嵌套 list"解决
- 试图用迭代写，被 "neighbors[0]/[1] 固定写死" 绊住
- set 存访问记录但需要拿新节点连邻居时拿不到，应该用 dict

### 💡 关键洞察
图的深拷贝 = DFS 遍历 + dict 缓存（旧→新映射），遇到已访问的节点直接从 dict 取出连上，不递归，断开循环。

### 🔍 触发特征
- 题目说"deep copy"、"clone" → 大概率是 DFS/BFS + map
- 输入是复杂对象/链表/图 → 不能直接赋值，需要新建节点 + 映射关系
- 有环/重复引用 → 需要一个 visited/cache 结构来打破循环

### 📌 一句话原则
**克隆类问题 = 遍历创建 + 映射缓存；先存再遍历（防环），遇到已缓存的直接取来连上。**

### ➡️ 同类变式
- 138. 随机链表的复制
- 1485. 克隆含随机指针的二叉树

>下一版
```python

```
