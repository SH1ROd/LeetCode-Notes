#哈希表
[1. 两数之和 - 力扣（LeetCode）](https://leetcode.cn/problems/two-sum/description/)
```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        map<int, int> v;
        vector<int> ans;
        int n = nums.size();
        for (int i = 0; i < n; i++) {
            if (v.find(nums[i]) == v.end()) {
                v[target - nums[i]] = i;
            } else {
                ans.push_back(v[nums[i]]);
                ans.push_back(i);
                return ans;
            }
        }
        return ans;
    }
};
```

>GPT改进
```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> mp;  // 改进1: 使用 unordered_map (平均 O(1) 查找)
        for (int i = 0; i < nums.size(); ++i) {
            int complement = target - nums[i];
            if (mp.count(complement)) { // 改进2: 如果补数已存在于哈希表中
                return {mp[complement], i}; // 改进3: 使用初始化列表构造 vector，更简洁
            }
            mp[nums[i]] = i;
        }
        return {};
    }
};
```

>宜均版本
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        ans = list()
        list_nums = len(nums)
        for i in range(list_nums):
	        diff = target - nums[i]
	        if (diff in nums) and (nums.index(diff) != i):
		        ans.extend([i, nums.index(diff)])
		        return ans
```

>GPT版本
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
	    seen = {}
        for i, num in enumerate(nums):
            diff = target - num
            if diff in seen:
                return(seen[diff], i)
            seen[num] = i
```

>2026年3月8日
```python
v = set()  
d = dict()  
for i, x in enumerate(nums):  
    if (target -x ) in v:  
        print([i, d[target -x][0]])  
    else:  
        v.add(x)  
        d[x] = []  
        d[x].append(i)
```