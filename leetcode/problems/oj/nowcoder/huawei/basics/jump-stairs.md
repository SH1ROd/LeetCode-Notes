#动态规划 
[跳台阶_牛客题霸_牛客网](https://www.nowcoder.com/practice/8c82a5b80378478f9484d87d1c5f12a4)
```c++
class Solution {
public:
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 
     * @param number int整型 
     * @return int整型
     */
    int jumpFloor(int number) {
        // write code here
        vector<int> dp(number + 1);
        dp[0] = 1;
        dp[1] = 1;
        for(int i=2;i<=number;i++){
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        // v[i] = v[i-1] + v[i - 2]
        return dp[number];
    }
};
```

```python
#
# 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
#
# 
# @param number int整型 
# @return int整型
#
class Solution:
    def jumpFloor(self , number: int) -> int:
        # write code here
        dp = [0] * (number + 1) # 新语法: list初始化长度和值
        dp[0] = 1
        dp[1] = 1
        for i in range(2, number + 1):
            dp[i] = dp[i - 1] + dp[i - 2]
        return dp[number]
```

> **新语法: list初始化长度和值**
```python
dp = [0] * (n + 1)
```