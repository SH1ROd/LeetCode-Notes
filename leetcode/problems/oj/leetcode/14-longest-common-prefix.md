#字符串
[14. 最长公共前缀 - 力扣（LeetCode）](https://leetcode.cn/problems/longest-common-prefix/)

>我的题解
```c++
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {

        int count = 0;
        string ans;

        for (int i = 0; i < strs[0].length(); i++){
            count = 0;
            for (int j = 0; j < strs.size(); j++){
                if (strs[0][i] != strs[j][i]){
                    break;
                } else {
                    count++;
                }
            }
            if (count == strs.size()){
                ans += strs[0][i];
            }
            else{
                return ans;
            }
        }

        return ans;
        
    }
};
```

>我的第二次题解
```c++
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        string ans = "";
        for(int j=0;j<strs[0].size();j++){
            int cnt=0;
            for(int i=1;i<strs.size();i++){
                if(strs[0][j] == strs[i][j]){
                    cnt++;
                }
            }
            if(cnt == strs.size() - 1){
                ans+=strs[0][j];
            }else{
                break;
            }
        }
        return ans;
    }
};
```
