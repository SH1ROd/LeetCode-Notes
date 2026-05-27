#滑动窗口 #动态规划 
[1871. 跳跃游戏 VII - 力扣（LeetCode）](https://leetcode.cn/problems/jump-game-vii/description/)

>失败-直觉版
```python
class Solution:
    def canReach(self, s: str, minJump: int, maxJump: int) -> bool:
        n = len(s)
        ans = False
        crr_step = 0
        for i in range(1, n):
            crr_step += 1
            if s[i] == '0':
                if minJump <= crr_step and crr_step <= maxJump:
                    ans = True
                    crr_step = 0
                else:
                    ans = False
                    break
        return ans
```

>吃力
```python
class Solution:
    def canReach(self, s: str, minJump: int, maxJump: int) -> bool:
        n = len(s)
        dp = [False] * n
        dp[0] = True
        # dp[i] = dp[i-maxJump] or ... dp[i-minJump]
        ans_cnt = 0
        for i in range(n):
            if i - minJump >= 0:
                ans_cnt += dp[i - minJump] 
            if i - maxJump > 0:
                ans_cnt -= dp[i - maxJump - 1]
            if ans_cnt > 0 and s[i] == '0':
                dp[i] =True
        return dp[n - 1]
        
```

>小吃力
```python
class Solution:
    def canReach(self, s: str, minJump: int, maxJump: int) -> bool:
        n = len(s)
        dp =[False] * n
        dp[0] = True
        range_true = 0 
        for i in range(n):
            if i - minJump >= 0:
                range_true += dp[i - minJump]
            if i - maxJump - 1 >= 0:
                range_true -= dp[i - maxJump - 1]
            if s[i] == '0' and range_true > 0:
                dp[i] = True
        return dp[n - 1]
```

>下一版
```python

```

>数学证明

# 一、先定义 DP 变量（形式化）

定义状态：

$$  
dp[k] = True  
$$

表示：

位置 k 可以从 0 跳到

初始条件：

$$  
dp[0] = True  
$$

---

# 二、题目原始跳跃规则

题目给出的规则：

$$  
minJump \le j-i \le maxJump  
$$

并且

$$  
s[j] = '0'  
$$

所以跳跃成立条件是：

$$  
(minJump \le j-i \le maxJump) \land (s[j]='0')  
$$

---

# 三、写出“正向”逻辑命题

如果：

- i 可达
    
- 且 i 能跳到 j
    

那么 j 可达。

写成逻辑：

$$  
dp[i] \land (minJump \le j-i \le maxJump) \land (s[j]='0') \Rightarrow dp[j]  
$$

意思：

如果存在一个 i 满足这些条件，那么 j 就可达

---

# 四、把“存在某个 i”写出来

上面其实隐含着存在某个 i，所以可以写成：

$$  
\exists i : dp[i] \land (minJump \le j-i \le maxJump) \land (s[j]='0')  
$$

推出：

$$  
dp[j] = True  
$$

---

# 五、把条件拆开

注意：

$$  
s[j]='0'  
$$

和 i 无关，只依赖 j。

所以可以把它提出来：

$$  
(s[j]='0') \land  
\left(  
\exists i : dp[i] \land (minJump \le j-i \le maxJump)  
\right)  
$$

---

# 六、把跳跃条件改写成区间

跳跃条件：

$$  
minJump \le j-i \le maxJump  
$$

代数变形：

$$  
j-maxJump \le i \le j-minJump  
$$

---

# 七、把条件代入

于是：

$$  
i \in [j-maxJump , j-minJump]  
$$

所以存在条件变成：

$$  
\exists i \in [j-maxJump , j-minJump]  
$$

---

# 八、代入到 DP

原来的存在条件：

$$  
\exists i : dp[i] \land (minJump \le j-i \le maxJump)  
$$

变成：

$$  
\exists i \in [j-maxJump , j-minJump] \quad dp[i]  
$$

---

# 九、把所有条件合并

再把之前拆开的 s[j] 条件合回去：

$$  
dp[j] = (s[j]='0') \land \left( \exists i \in [j-maxJump , j-minJump] \ dp[i]=True \right)  
$$

---

# 十、最终含义

j 可达，当且仅当：

1. j 是 '0'
    
2. 在区间 [j-maxJump , j-minJump] 里存在一个可达位置
    

---

# 十一、再写成“区间查询问题”

$$  
dp[j] = (s[j]='0') \land (\text{区间}[j-maxJump , j-minJump] \text{存在True})  
$$

也就是区间存在性问题

---

# 十二、这一步为什么是关键

把问题从：

i → j

变成：

j ← i

于是判断 j 是否可达只需要看一个区间

于是可以用：

- 滑动窗口
    
- 前缀和
    
- 线段树
    

来优化

---

# 十三、整个推导链（完整公式）

$$  
dp[i] \land (minJump \le j-i \le maxJump) \land (s[j]='0') \Rightarrow dp[j]  
$$

$$  
\exists i : dp[i] \land (minJump \le j-i \le maxJump)  
$$

$$  
\exists i \in [j-maxJump , j-minJump] \ dp[i]  
$$

$$  
dp[j] = (s[j]='0') \land \left( \exists i \in [j-maxJump , j-minJump] \ dp[i] \right)  
$$

---

# 十四、这一类 DP 的统一抽象

$$  
dp[j] = (s[j]='0') \land Query(dp[L(j) ... R(j)])  
$$

其中 Query = 是否存在 True

这就是为什么可以用滑动窗口统计 True 数量。

---
