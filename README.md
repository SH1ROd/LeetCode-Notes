<p align="center">
  <a href="#简体中文">简体中文</a> ·
  <a href="#繁體中文">繁體中文</a> ·
  <a href="#english">English</a>
</p>

---

<a name="简体中文"></a>

# LeetCode 刷题笔记

> 刷题记录 · 方法论沉淀 · 面试准备

---

## 📊 刷题总览

| 指标 | 数值 |
|------|------|
| LeetCode 主库 | 41 题 |
| 面试真题（滴滴/米哈游/拼多多/小红书/招行） | 19 题 |
| Nowcoder 华为 | 12 题 |
| 覆盖算法标签 | 14+ 个 |
| 有方法论沉淀的题目 | 17 题 |
| 有错误分析/多版本演进的题目 | 13 题 |

**难度分布：** Easy 12 · Medium 28 · Hard 1 · **语言分布：** Python 为主，部分 C++

---

## 📈 多维度能力评估

```
                     图/树/DFS/BFS (0)
                         │
                   0     │     10
                  ┌──────┼──────┐
     哈希表/字符串 │  6   │  8   │ 滑动窗口/双指针
       (6)        │      │      │    (8)
                  │      │      │
                  │  9   │  7   │
       栈/链表 ───┤      │      ├─── 前缀和/差分
       (3)       │      │      │      (7)
                  │  7   │  2   │
                  │      │      │
      DP-区间/线性 │  9   │  0   │ 优先队列/二分
       (7)        └──────┴──────┘      (2)
                      │
                   10     │
                     图论完全空白
```

### 各维度详解

#### 🟢 滑动窗口 / 双指针 — 8/10
8 题。系统掌握了通用模板（右扩找条件、左缩减优化），209、1658、1695 中有标准化方法论，1871 有 DP 转区间查询的完整推导。

#### 🟢 动态规划-背包 — 9/10
8 题。覆盖 0/1 背包、完全背包、二维背包、计数/最优化/存在型，对内外层循环语义理解深入。377 有排列 vs 组合决策表，416 有布尔 DP vs 价值 DP 触发器，494 有 8 条错误反思。

#### 🟡 前缀和 / 差分数组 — 7/10
7 题。差分数组有四句七字口诀：差分长度要加一，首位不变后减前。左标原位右加一，前缀求和只看 N。

#### 🟡 DP-区间调度 / 线性DP — 7/10
6 题。区间调度类已形成套路（排序 + 二分转移 + DP），650 展示了暴力→数学优化的四阶段思考。

#### 🟡 哈希表 / 字符串 — 6/10
7 题。3Sum 的哈希→双指针演进详细，但缺少 hard 级复杂处理。

#### 🔴 栈 / 链表 — 3/10
4 题。只有最基础的括号匹配、链表合并、相交链表。单调栈是面试高频，尚未覆盖。

#### 🔴 优先队列 / 二分 — 2/10
3 题。缺少 Top-K、数据流中位数、旋转数组等经典题型。

#### ⚫ 图 / 树 / DFS / BFS — 0/10
0 题。最大空白区。

---

## 🎯 刷题建议

### P0 — 求职必考，当前空白
1. 🌲 **二叉树**：遍历 · 构建 · LCA · 序列化（建议 94/102/105/236/297，预计 5-7 题）
2. 🔙 **回溯**：排列 · 组合 · 子集 · 棋盘（建议 46/78/39/51/22，预计 5 题）
3. 📈 **单调栈**：下个更大元素 · 接雨水 · 柱状图（建议 739/42/84，预计 3 题）
4. 🌐 **图**：拓扑排序 · 最短路 · 并查集（建议 207/743/200/547，预计 5 题）

### P1 — 巩固弱项
5. **二分查找**：边界处理 · 旋转数组（33/34/153/74，预计 4 题）
6. **优先队列**：Top-K · 数据流 · 区间合并（215/295/56/347，预计 4 题）
7. **栈/链表进阶**：LRU · 链表反转 · 单调栈（146/206/445）

### P2 — 强化优势
8. **DP 进阶**：状态压缩 · 树形 DP（短板补完后拓展）

---

## 🧠 方法论沉淀

| 方法论 | 所在文件 | 类型 |
|--------|---------|------|
| 滑动窗口通用模板 | 209-minimum-size-subarray-sum | 模板 + 迁移表 |
| 滑动窗口四句口诀 | 1695-maximum-erasure-value | 口诀 |
| 差分数组 0 索引口诀 | 3355-zero-array-transformation-i | 口诀 |
| 背包 DP 循环顺序决策表 | 377-combination-sum-iv | 决策表 |
| 布尔 DP vs 价值 DP 触发器 | 416-partition-equal-subset-sum | 流程判断 |
| 二分查找边界速查表 | 2008-maximum-earnings-from-taxi | 速查表 |
| 8 条常见 DP 思维错误 | 494-target-sum | 错误清单 |
| 算法 8 句口诀 | docs/algorithm-handbook.md | 口诀 |

**建议整理但尚未沉淀的：** 哈希表常用技巧（计数 vs 索引 vs 去重）、双指针通用模板（同向/相向/快慢）、链表反转与递归框架、回溯模板（选择→递归→撤销）

---

## 📝 近期刷题

| 题目 | 标签 | 要点 |
|------|------|------|
| 3194. 最小元素和最大元素的平均值 | #哈希表 | min/max 移除求均值 |
| 2465. 统计不同平均值数目 | #哈希表 | 同上思路，去重版本 |
| 5. 最长回文子串 | #字符串 | 中心扩展法，边界条件 |
| 2518. 好分区数目 | #背包 #DP #计数 #容斥 | 容斥 + 组合 |
| 2402. 会议室 III | #优先队列 | 未完成 |
| 2054. 两个最好的不重叠活动 | #DP #区间调度 | 二分+DP |
| 2008. 出租车最大盈利 | #DP #区间调度 | 同上模式 |
| 1871. 跳跃游戏 VII | #滑动窗口 #DP | DP→区间查询推导 |
| 1695. 删除子数组的最大得分 | #滑动窗口 | 滑动窗口通用模板 |
| 1658. 将 x 减到 0 的最小操作数 | #滑动窗口 | 双向滑动窗口 |

---

## 💼 求职准备

| 维度 | 状态 |
|------|------|
| 数据结构（数组/哈希/字符串） | ✅ 基础扎实 |
| 数据结构（栈/队列/链表） | ⚠️ 需补充 |
| 算法（滑动窗口/双指针） | ✅ 强项 |
| 算法（前缀和/差分） | ✅ 扎实 |
| 算法（二分/排序） | ❌ 薄弱 |
| 算法（DFS/BFS/图） | ❌ 未覆盖 |
| 算法（回溯/递归） | ❌ 未覆盖 |
| 动态规划（背包） | ✅ 强项 |
| 动态规划（区间/线性） | ✅ 扎实 |
| 动态规划（树形/状态压缩） | ❌ 未覆盖 |

**面试公司覆盖：** 滴滴 ✅ 米哈游 ✅ 拼多多 ✅ 小红书 ✅ 招商银行 ✅

**当前阶段：** 基础入门 ~55% · 方法论沉淀 ~70% · 弱项补齐 ~20% · 面试模拟 ~5%

---

## 🗺️ 项目地图

```
leetcode/
├── problems/
│   ├── oj/
│   │   ├── leetcode/          ← 主刷目录 (41题)
│   │   ├── nowcoder/huawei/   (12题)
│   │   └── sphere-oj/
│   └── interviews/            (19题)
│       ├── didi/ · mihoyo/ · pdd/ · xiaohongshu/ · cmb-network/ · cmb-cloud/
└── docs/
    ├── algorithm-handbook.md  ·  interview-tags.md
    ├── python/ · java/ · templates/
```

---

<p align="center">
  <a href="#简体中文">↑ 回到顶部</a>
</p>

---

<a name="繁體中文"></a>

# LeetCode 刷題筆記

> 刷題記錄 · 方法論沉澱 · 面試準備

---

## 📊 刷題總覽

| 指標 | 數值 |
|------|------|
| LeetCode 主庫 | 41 題 |
| 面試真題（滴滴/米哈游/拼多多/小紅書/招行） | 19 題 |
| Nowcoder 華為 | 12 題 |
| 覆蓋演算法標籤 | 14+ 個 |
| 有方法論沉澱的題目 | 17 題 |
| 有錯誤分析/多版本演進的題目 | 13 題 |

**難度分佈：** Easy 12 · Medium 28 · Hard 1 · **語言分佈：** Python 為主，部分 C++

---

## 📈 多維度能力評估

```
                     圖/樹/DFS/BFS (0)
                         │
                   0     │     10
                  ┌──────┼──────┐
     哈希表/字串  │  6   │  8   │ 滑動視窗/雙指針
       (6)        │      │      │    (8)
                  │      │      │
                  │  9   │  7   │
       棧/鏈表 ───┤      │      ├─── 前綴和/差分
       (3)       │      │      │      (7)
                  │  7   │  2   │
                  │      │      │
      DP-區間/線性 │  9   │  0   │ 優先佇列/二分
       (7)        └──────┴──────┘      (2)
                      │
                   10     │
                     圖論完全空白
```

### 各維度詳解

#### 🟢 滑動視窗 / 雙指針 — 8/10
8 題。系統掌握通用模板，209、1658、1695 有標準化方法論，1871 有 DP 轉區間查詢的完整推導。

#### 🟢 動態規劃-背包 — 9/10
8 題。覆蓋 0/1 背包、完全背包、二維背包、計數/最優化/存在型，對內外層循環語義理解深入。

#### 🟡 前綴和 / 差分陣列 — 7/10
7 題。差分陣列有四句七字口訣。

#### 🟡 DP-區間排程 / 線性DP — 7/10
6 題。區間排程已形成套路（排序 + 二分轉移 + DP）。

#### 🟡 哈希表 / 字串 — 6/10
7 題。3Sum 的哈希→雙指針演進詳細。

#### 🔴 棧 / 鏈表 — 3/10
4 題。只有最基礎的括號匹配、鏈表合併。

#### 🔴 優先佇列 / 二分 — 2/10
3 題。缺少 Top-K、資料流中位數等經典題型。

#### ⚫ 圖 / 樹 / DFS / BFS — 0/10
0 題。最大空白區。

---

## 🎯 刷題建議

### P0 — 求職必考，當前空白
1. 🌲 **二元樹**：遍歷 · 構建 · LCA · 序列化
2. 🔙 **回溯**：排列 · 組合 · 子集 · 棋盤
3. 📈 **單調棧**：下個更大元素 · 接雨水 · 柱狀圖
4. 🌐 **圖**：拓撲排序 · 最短路 · 並查集

### P1 — 鞏固弱項
5. **二分搜尋**：邊界處理 · 旋轉陣列
6. **優先佇列**：Top-K · 資料流 · 區間合併
7. **棧/鏈表進階**：LRU · 鏈表反轉

### P2 — 強化優勢
8. **DP 進階**：狀態壓縮 · 樹形 DP

---

## 🧠 方法論沉澱

| 方法論 | 檔案 | 類型 |
|--------|------|------|
| 滑動視窗通用模板 | 209-minimum-size-subarray-sum | 模板 |
| 滑動視窗口訣 | 1695-maximum-erasure-value | 口訣 |
| 差分陣列口訣 | 3355-zero-array-transformation-i | 口訣 |
| 背包 DP 循環順序決策表 | 377-combination-sum-iv | 決策表 |
| 二分搜尋邊界速查表 | 2008-maximum-earnings-from-taxi | 速查表 |
| 8 條常見 DP 思維錯誤 | 494-target-sum | 錯誤清單 |
| 演算法 8 句口訣 | docs/algorithm-handbook.md | 口訣 |

---

## 💼 求職準備

| 維度 | 狀態 |
|------|------|
| 資料結構（陣列/哈希/字串） | ✅ 基礎紮實 |
| 資料結構（棧/佇列/鏈表） | ⚠️ 需補充 |
| 演算法（滑動視窗/雙指針） | ✅ 強項 |
| 演算法（前綴和/差分） | ✅ 紮實 |
| 演算法（二分/排序） | ❌ 薄弱 |
| 演算法（DFS/BFS/圖） | ❌ 未覆蓋 |
| 演算法（回溯/遞迴） | ❌ 未覆蓋 |
| 動態規劃（背包） | ✅ 強項 |
| 動態規劃（區間/線性） | ✅ 紮實 |
| 動態規劃（樹形/狀態壓縮） | ❌ 未覆蓋 |

---

<p align="center">
  <a href="#简体中文">简体中文</a> · <a href="#繁體中文">↑ 回到顶部</a> · <a href="#english">English</a>
</p>

---

<a name="english"></a>

# LeetCode Notes

> Practice Log · Methodology Notes · Interview Prep

---

## 📊 Overview

| Metric | Count |
|--------|-------|
| LeetCode (main) | 41 problems |
| Interview真题 (Didi/Mihoyo/PDD/Xiaohongshu/CMB) | 19 problems |
| Nowcoder Huawei | 12 problems |
| Algorithm tags covered | 14+ |
| Problems with methodology notes | 17 |
| Problems with wrong-version analysis | 13 |

**Difficulty:** Easy 12 · Medium 28 · Hard 1 · **Languages:** Python (primary), some C++

---

## 📈 Multi-Dimension Assessment

```
                    Graph/Tree/DFS/BFS (0)
                         │
                   0     │     10
                  ┌──────┼──────┐
     Hash/String  │  6   │  8   │ Sliding Window/
       (6)        │      │      │ Two Pointers (8)
                  │      │      │
                  │  9   │  7   │
    Stack/Linked ─┤      │      ├─── Prefix Sum/
     List (3)     │      │      │ Difference Array (7)
                  │  7   │  2   │
                  │      │      │
   DP-Interval/   │  9   │  0   │ Heap/Binary
    Linear (7)    └──────┴──────┘ Search (2)
                      │
                   10     │
                  Graph: completely blank
```

### Dimension Breakdown

#### 🟢 Sliding Window / Two Pointers — 8/10
8 problems. Mastered the universal template. 209, 1658, 1695 contain standardized methodology. 1871 has a full derivation from DP recurrence to interval queries.

#### 🟢 DP-Knapsack — 9/10
8 problems. Covers 0/1 knapsack, unbounded knapsack, 2D knapsack, counting/optimization/existence variants. Deep understanding of nested loop semantics. 377 has a permutation vs combination decision table, 416 has a boolean vs max-value DP trigger guide.

#### 🟡 Prefix Sum / Difference Array — 7/10
7 problems. The difference array has a 4-line mnemonic for zero-indexed writing.

#### 🟡 DP-Interval Scheduling / Linear DP — 7/10
6 problems. Formed a repeatable pattern: sort + binary search transition + DP. 650 demonstrates a 4-stage evolution from brute force to mathematical optimization.

#### 🟡 Hash Table / String — 6/10
7 problems. 3Sum hash→two-pointer evolution is well documented, but lacks hard-level complex string problems.

#### 🔴 Stack / Linked List — 3/10
4 problems. Only basic parentheses, merge lists, intersection. Monotonic stack (a high-frequency interview topic) not covered.

#### 🔴 Heap / Binary Search — 2/10
3 problems. Missing classic problems like Top-K, median of data stream, rotated array search.

#### ⚫ Graph / Tree / DFS / BFS — 0/10
0 problems. Biggest gap.

---

## 🎯 Recommendations

### P0 — Required for interviews, currently missing
1. 🌲 **Binary Tree**: traversal · construction · LCA · serialization
2. 🔙 **Backtracking**: permutations · combinations · subsets · board
3. 📈 **Monotonic Stack**: next greater element · trapping rain · histogram
4. 🌐 **Graph**: topological sort · shortest path · union find

### P1 — Reinforce weaknesses
5. **Binary Search**: boundary handling · rotated array
6. **Heap**: Top-K · data stream median · interval merge
7. **Stack/Linked List**: LRU · reverse list

### P2 — Build on strengths
8. **Advanced DP**: state compression · tree DP

---

## 🧠 Methodology Notes

| Topic | File | Type |
|-------|------|------|
| Sliding window template | 209-minimum-size-subarray-sum | template |
| Sliding window mnemonic | 1695-maximum-erasure-value | mnemonic |
| Difference array mnemonic | 3355-zero-array-transformation-i | mnemonic |
| Knapsack loop order table | 377-combination-sum-iv | decision table |
| Boolean vs value DP guide | 416-partition-equal-subset-sum | flowchart |
| Binary search boundary ref | 2008-maximum-earnings-from-taxi | quick reference |
| 8 common DP mistakes | 494-target-sum | error checklist |
| Algorithm 8-liner | docs/algorithm-handbook.md | mnemonic |

---

## 💼 Job Hunt Readiness

| Dimension | Status |
|-----------|--------|
| Data Structures (Array/Hash/String) | ✅ Solid |
| Data Structures (Stack/Queue/LinkedList) | ⚠️ Need work |
| Algorithms (SlidingWindow/TwoPointers) | ✅ Strong |
| Algorithms (PrefixSum/DiffArray) | ✅ Solid |
| Algorithms (BinarySearch/Sorting) | ❌ Weak |
| Algorithms (DFS/BFS/Graph) | ❌ Not covered |
| Algorithms (Backtracking/Recursion) | ❌ Not covered |
| DP (Knapsack) | ✅ Strong |
| DP (Interval/Linear) | ✅ Solid |
| DP (Tree/StateCompression) | ❌ Not covered |

**Interview coverage:** Didi ✅ Mihoyo ✅ PDD ✅ Xiaohongshu ✅ CMB ✅

---

<p align="center">
  <a href="#简体中文">简体中文</a> · <a href="#繁體中文">繁體中文</a> · <a href="#english">↑ Back to top</a>
</p>
