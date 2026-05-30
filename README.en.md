<p align="center">
  <a href="README.md">简体中文</a> ·
  <a href="README.zh-TW.md">繁體中文</a> ·
  <a href="README.en.md">English</a>
</p>

---

# LeetCode Notes

> Practice Log · Methodology Notes · Interview Prep

---

## 📊 Overview

| Metric | Count |
|--------|-------|
| LeetCode (main) | 41 problems |
| Interview problems (Didi/Mihoyo/PDD/Xiaohongshu/CMB) | 19 |
| Nowcoder Huawei | 12 |
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
8 problems. Mastered the universal template (expand right to satisfy condition, shrink left to optimize). 209, 1658, 1695 contain standardized methodology. 1871 has a full derivation from DP recurrence to interval queries.

#### 🟢 DP-Knapsack — 9/10
8 problems. Covers 0/1 knapsack, unbounded knapsack, 2D knapsack, counting/optimization/existence variants. Deep understanding of nested loop semantics. 377 has a permutation vs combination decision table, 416 has a boolean vs max-value DP trigger guide, 494 lists 8 common DP mistakes.

#### 🟡 Prefix Sum / Difference Array — 7/10
7 problems. Difference array has a 4-line, 7-char-per-line mnemonic for zero-indexed writing.

#### 🟡 DP-Interval Scheduling / Linear DP — 7/10
6 problems. Formed a repeatable pattern: sort + binary search transition + DP. 650 demonstrates a 4-stage evolution from brute force to mathematical optimization.

#### 🟡 Hash Table / String — 6/10
7 problems. 3Sum hash→two-pointer evolution is well documented, but lacks hard-level complex string problems.

#### 🔴 Stack / Linked List — 3/10
4 problems. Only basic parentheses matching, merge lists, intersection. Monotonic stack (a high-frequency interview topic) not covered.

#### 🔴 Heap / Binary Search — 2/10
3 problems. Missing classic problems like Top-K, median of data stream, rotated array search.

#### ⚫ Graph / Tree / DFS / BFS — 0/10
0 problems. Biggest gap.

---

## 🎯 Recommendations

### P0 — Required for interviews, currently missing
1. 🌲 **Binary Tree**: traversal · construction · LCA · serialization (try 94/102/105/236/297, ~5-7 problems)
2. 🔙 **Backtracking**: permutations · combinations · subsets · board (46/78/39/51/22, ~5 problems)
3. 📈 **Monotonic Stack**: next greater element · trapping rain · histogram (739/42/84, ~3 problems)
4. 🌐 **Graph**: topological sort · shortest path · union find (207/743/200/547, ~5 problems)

### P1 — Reinforce weaknesses
5. **Binary Search**: boundary handling · rotated array (33/34/153/74, ~4 problems)
6. **Heap**: Top-K · data stream median · interval merge (215/295/56/347, ~4 problems)
7. **Stack/Linked List**: LRU · reverse list · monotonic stack (146/206/445)

### P2 — Build on strengths
8. **Advanced DP**: state compression · tree DP (after filling gaps)

---

## 🧠 Methodology Notes

| Topic | File | Type |
|-------|------|------|
| Sliding window template | 209-minimum-size-subarray-sum | template + migration table |
| Sliding window mnemonic | 1695-maximum-erasure-value | mnemonic |
| Difference array mnemonic | 3355-zero-array-transformation-i | mnemonic |
| Knapsack loop order table | 377-combination-sum-iv | decision table |
| Boolean vs value DP guide | 416-partition-equal-subset-sum | flowchart |
| Binary search boundary ref | 2008-maximum-earnings-from-taxi | quick reference |
| 8 common DP mistakes | 494-target-sum | error checklist |
| Algorithm 8-liner | docs/algorithm-handbook.md | mnemonic |

**To be summarized:** hash table patterns (counting vs indexing vs dedup), two-pointer templates (same-direction/opposite/fast-slow), linked list reversal & recursion framework, backtracking template (choose → recurse → undo)

---

## 📝 Recent Problems

| Problem | Tags | Key Point |
|---------|------|-----------|
| 3194. Min Average of Smallest & Largest | #hash-table | min/max removal average |
| 2465. Number of Distinct Averages | #hash-table | same approach, dedup version |
| 5. Longest Palindromic Substring | #string | center expansion, boundary |
| 2518. Number of Good Partitions | #knapsack #DP #counting | inclusion-exclusion |
| 2402. Meeting Rooms III | #heap | incomplete |
| 2054. Two Best Non-Overlapping Events | #DP #interval-scheduling | binary search + DP |
| 2008. Max Earnings from Taxi | #DP #interval-scheduling | same pattern |
| 1871. Jump Game VII | #sliding-window #DP | DP→interval query derivation |
| 1695. Maximum Erasure Value | #sliding-window | universal sliding window template |
| 1658. Min Operations to Reduce X to Zero | #sliding-window | bidirectional sliding window |

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

**Current phase:** Fundamentals ~55% · Methodology ~70% · Filling gaps ~20% · Mock interviews ~5%

---

## 🗺️ Project Map

```
leetcode/
├── problems/
│   ├── oj/
│   │   ├── leetcode/          ← main directory (41 problems)
│   │   ├── nowcoder/huawei/   (12 problems)
│   │   └── sphere-oj/
│   └── interviews/            (19 problems)
│       ├── didi/ · mihoyo/ · pdd/ · xiaohongshu/ · cmb-network/ · cmb-cloud/
└── docs/
    ├── algorithm-handbook.md  ·  interview-tags.md
    ├── python/ · java/ · templates/
```

---

## 📖 Usage Guide

All skills trigger via natural language — no slash commands needed.

**Practice mode** — just say "practice" or "solve problem X":

> practice two-sum
> solve 209 用了滑动窗口但结果不对
> https://leetcode.cn/problems/3sum/

**Two modes, auto-selected:**

| Your status | Mode | Behavior |
|------------|------|----------|
| Solved first try | ✅ Quick | Auto-format note + optional summary |
| Stuck / wrong | 🔄 Deep | Diagnose → escalating hints → solve → personal migration card |

Output: A note documenting the full thought evolution + a transferable personal methodology card.

**Update stats** — say "update README" or "refresh progress" to rescan the codebase.

---

<p align="center">
  <a href="README.md">简体中文</a> ·
  <a href="README.zh-TW.md">繁體中文</a>
</p>
