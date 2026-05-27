#动态规划 
[718. 最长重复子数组 - 力扣（LeetCode）](https://leetcode.cn/problems/maximum-length-of-repeated-subarray/description/)

```c++
class Solution {
public:
    int findLength(vector<int>& nums1, vector<int>& nums2) {
        int n1 = nums1.size();
        int n2 = nums2.size();
        int ans = 0;
        vector<vector<int>> dp(n1+1, vector<int>(n2+1));
        for(int i=1;i<=n1;i++){
            for(int j=1;j<=n2;j++){
                if(nums1[i-1]==nums2[j-1]){
                    dp[i][j]=dp[i-1][j-1] + 1;
                    ans = max(dp[i][j], ans);
                }
                else{
                    dp[i][j]=0;
                }
            }
        }
        return ans;
    }
};
```

> 2025年6月9日
```c++
class Solution {
public:
    int findLength(vector<int>& nums1, vector<int>& nums2) {
        int n1 = nums1.size();
        int n2 = nums2.size();
        int ans = 0;
        vector<vector<int>> dp(n1 + 1, vector<int>(n2 + 1));
        for(int i=1;i<=n1;i++){
            for(int j=1;j<=n2;j++){
                if(nums1[i-1]==nums2[j-1]){
                    dp[i][j] = dp[i-1][j-1] + 1;
                }
                if (dp[i][j] > ans){
                    ans = dp[i][j];
                }
            }
        }
        return ans;

    }
};
```