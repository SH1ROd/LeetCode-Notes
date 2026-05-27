#哈希表 
[两数之和_牛客题霸_牛客网](https://www.nowcoder.com/practice/20ef0972485e41019e39543e8e895b7f?tpId=196&tqId=37090&ru=/exam/oj)
```c++
class Solution {
public:
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 
     * @param numbers int整型vector 
     * @param target int整型 
     * @return int整型vector
     */
    vector<int> twoSum(vector<int>& numbers, int target) {
        // write code here
        unordered_map<int, int> m;
        for(int i=0;i<numbers.size();i++){
            if(m.count(target - numbers[i])==0){
                m[numbers[i]] = i;
            }
            else{
                return {m[target - numbers[i]] + 1, i + 1};
            }
        }
        return {-1, -1};
    }
};
```

```python
#
# 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
#
# 
# @param numbers int整型一维数组 
# @param target int整型 
# @return int整型一维数组
#
class Solution:
    def twoSum(self , numbers: List[int], target: int) -> List[int]:
        # write code here
        v = {}
        for i in range(len(numbers)):
            if target - numbers[i] not in v:
                v[numbers[i]] = i
            else:
                return [v[target - numbers[i]] + 1, i + 1]
        return [-1, -1]
```

>len()就是.size()
```python
for i in range(len(numbers)):
```