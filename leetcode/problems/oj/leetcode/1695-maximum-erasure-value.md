#滑动窗口 
[1695. 删除子数组的最大得分 - 力扣（LeetCode）](https://leetcode.cn/problems/maximum-erasure-value/description/)

```c++
class Solution {
public:
    int maximumUniqueSubarray(vector<int>& nums) {
        set<int> v;
        int r = 0;
        int ans = 0;
        int sum = 0;
        int n = nums.size();
        if (n==1){
            return nums[0];
        }
        for(int i=0;i<n;i++){
            while (r<n && v.find(nums[r])==v.end()){
                v.insert(nums[r]);
                sum+=nums[r];
                ans = max(ans, sum);
                r++;
            }
            v.erase(nums[i]);
            sum-=nums[i];
        }
        return ans;
    }
};
```

>下一版待续:
```python

```


> 错误版：
> 第一版（核心问题：窗口状态不同步 + 没删除重复元素）

```python
class Solution:
    def maximumUniqueSubarray(self, nums: List[int]) -> int:
        n = len(nums)
        l = 0
        cur_sum = 0
        cur_nums = set()  # 用set维护窗口元素
        max_sum = -1

        for r in range(n):

            # 🧠 思路：如果新元素不重复就加入窗口
            if nums[r] not in cur_nums:
                cur_nums.add(nums[r])
                cur_sum += nums[r]
                max_sum = max(max_sum, cur_sum)

            else:
                # 🧠 思路：如果重复就移动左指针直到重复消失
                while nums[r] != nums[l]:

                    # ❌ 问题1：你只减少了sum
                    cur_sum -= nums[l]

                    # ❌ 但没有从set里删除
                    # cur_nums.remove(nums[l])  ←缺失

                    l += 1

                # ❌ 问题2：循环结束时
                # nums[l] == nums[r]
                # 但这个重复元素并没有被删除

        return max_sum
```

> 第二版（进步：意识到要同步删除）

```python
class Solution:
    def maximumUniqueSubarray(self, nums: List[int]) -> int:
        n = len(nums)
        l = 0
        cur_sum = 0
        cur_nums = set()
        max_sum = -1

        for r in range(n):

            # 🧠 思路：如果不重复就加入窗口
            if nums[r] not in cur_nums:
                cur_nums.add(nums[r])
                cur_sum += nums[r]
                max_sum = max(max_sum, cur_sum)

            else:
                # 🧠 思路：移动左指针直到找到重复元素
                while nums[r] != nums[l]:

                    # ✅ 改进：开始同步维护set
                    cur_nums.remove(nums[l])

                    cur_sum -= nums[l]
                    l += 1

                # 🧠 思路：最后再删掉重复的那个
                cur_nums.remove(nums[l])
                cur_sum -= nums[l]

        return max_sum
```

>最终版本（正确滑动窗口）

```python
class Solution:
    def maximumUniqueSubarray(self, nums: List[int]) -> int:
        n = len(nums)
        l = 0
        cur_sum = 0

        # ✅ 使用dict记录次数
        cur_nums = dict()

        max_sum = -1

        for r in range(n):

            # ✅ 第一步：右指针扩展窗口
            cur_sum += nums[r]

            # 记录元素出现次数
            cur_nums[nums[r]] = cur_nums.get(nums[r], 0) + 1

            # 🧠 如果出现重复
            while cur_nums[nums[r]] == 2:

                # ✅ 左指针缩小窗口
                cur_nums[nums[l]] -= 1
                cur_sum -= nums[l]
                l += 1

            # ✅ 窗口合法后更新答案
            max_sum = max(max_sum, cur_sum)

        return max_sum
```

# 你的思维演化路径（非常典型）

|版本|思考方式|问题|
|---|---|---|
|第一版|手动修补窗口|状态不同步|
|第二版|开始维护窗口结构|结构逻辑不完整|
|最终版|接受滑动窗口模板|正确|

你的问题不是不会。

而是：

```
没有先用模板
而是自己设计逻辑
```

---

# 滑动窗口通用模板（算法手册版）

所有滑动窗口题都可以套：

```
窗口 + 条件 + 最优值
```

模板：

```python
l = 0
window = {}
ans = 0

for r in range(n):

    # 1 扩窗口
    add(nums[r])

    # 2 修窗口
    while window不合法:
        remove(nums[l])
        l += 1

    # 3 更新答案
    ans = update(ans)
```

---

# 套到本题

窗口条件：

```
不能有重复元素
```

代码：

```python
while count[nums[r]] > 1:
```

---

# 滑窗思想钢印（强烈建议记住）

看到这些关键词：

```
连续
子数组
子串
最长
最短
最大
最小
```

第一反应：

```
滑动窗口
```

模板口诀：

```
右指针扩张
左指针收缩
窗口合法
更新答案
```

---

# 正确的滑动窗口思维

> 核心模板：
> 
> for r:  
>     while 窗口不合法:  
>         shrink left  
>     expand right  
>     更新答案
