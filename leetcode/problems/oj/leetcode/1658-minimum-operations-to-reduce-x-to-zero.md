#滑动窗口 
[1658. 将 x 减到 0 的最小操作数 - 力扣（LeetCode）](https://leetcode.cn/problems/minimum-operations-to-reduce-x-to-zero/)

> 2025年6月4日11:59:32
> 转化问题-->滑动窗口
```c++
class Solution {
public:
    int minOperations(vector<int>& nums, int x) {
        int n = nums.size();
        int sum = 0;
        for(int i=0;i<n;++i){
            sum += nums[i];
        }
        int target = sum - x;
        if(target == 0){
            return n;
        }else if(target < 0){
            return -1;
        }
        int right = -1;
        int now = 0;
        int min_len = n;
        for(int i=0;i<n;i++){
            while(right < n-1 && now <target){
                right++;
                now += nums[right];
            }
            if(now == target){
                // cout << i << ":" << right << endl;
                // cout << "now: " << now << endl;
                min_len = min(min_len, n - (right - i + 1));
            }
            now -= nums[i];
        }
        if(min_len == n){
            return -1;
        }
        else{
            return min_len;
        }
    }
};
```


>下一版待续
```python
```

>错误的版本
>第一版（没过）**

```python
class Solution:
    def minOperations(self, nums: List[int], x: int) -> int:
        n = len(nums)
        t = sum(nums)
        target = t - x  # 转化目标：保留子数组和 = sum(nums) - x
        t2 = 0
        r = 0
        ans = 0  # 问题1：初始化为0，无解时返回 n - ans 会错误

        # 外循环左指针，内循环右指针
        for l in range(n):
            t2 += nums[r]  # 问题2：第一次 for l 循环就加 nums[r]，r=0 → 第一次累加重复
            while t2 < target:  # 问题3：条件 t2 < target，右指针右移时可能越界
                r += 1
                t2 += nums[r]  # 问题4：r 越界没有检查
            if t2 == target:
                ans = max(ans, r - l + 1)
            t2 -= nums[l]  # 缩左指针

        if ans == 0: 
            return -1  # 问题5：ans初始化为0，和长度可能混淆
        return n - ans
```

>第二版（没过，但思路接近）

```python
class Solution: 
    def minOperations(self, nums: List[int], x: int) -> int:
        n = len(nums)
        t = sum(nums)
        target = t - x
        t2 = 0
        l = 0
        ans = 0  # 问题：初始化为0，无解时返回 n - ans 可能错误

        # 标准滑动窗口思路：右指针循环，左指针缩小窗口
        for r in range(n):
            t2 += nums[r]  # 右指针累加窗口和

            while t2 > target and l <= r:  # 缩左指针直到 sum <= target
                t2 -= nums[l]
                l += 1

            if t2 == target:
                ans = max(ans, r - l + 1)  # 更新最长子数组长度

        if ans == 0:  # 问题：ans初始化为0，无法区分无解
            return -1
        return n - ans
```


>第三版（现在通过版）

```python
class Solution:
    def minOperations(self, nums: List[int], x: int) -> int:
        n = len(nums)
        t = sum(nums)
        target = t - x  # 核心转换：保留最长子数组和 = sum(nums) - x
        t2 = 0
        l = 0
        ans = -1  # 正确初始化，无解时ans=-1

        # 滑动窗口模板
        for r in range(n):  
            t2 += nums[r]  # 右指针扩张窗口

            while t2 > target and l <= r:  # 条件不满足时缩左指针
                t2 -= nums[l]
                l += 1

            if t2 == target:  # 窗口满足条件，更新最长子数组长度
                ans = max(ans, r - l + 1)

        if ans == -1:  # 无解直接返回 -1
            return -1
        return n - ans  # 最少操作次数 = 总长度 - 保留的最长子数组长度
```

---

# 方法论点评

- **第一版**：试图手动控制左右指针，逻辑复杂 → 易越界、重复累加
    
- **第二版**：思路接近滑动窗口模板，但 ans 初始化不安全，边界情况未处理
    
- **第三版**：标准模板，**可迁移**到所有“最长/最短连续子数组/子串”问题
    

> 核心可迁移性：**滑动窗口 + 条件判断 + 动态维护最优解**

---

# 如何纠正你的思路

1. **初始化 ans/max_len 用 -1 或 inf**，不要用 0
    
2. **无解直接判断**，统一 return -1
    
3. **使用标准滑动窗口模板**，右指针循环，左指针缩小窗口
    
4. **不要 for l + while r 的手动控制**，容易越界/重复累加
    
5. **先抽象问题** → 转化为连续子数组问题再套模板
