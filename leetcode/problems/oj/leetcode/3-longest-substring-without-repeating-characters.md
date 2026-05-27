#滑动窗口 
[3. 无重复字符的最长子串 - 力扣（LeetCode）](https://leetcode.cn/problems/longest-substring-without-repeating-characters/description/)
```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int n = s.length();
        int r = 0;
        int ans = 0;
        set<int> v;
        for (int i=0;i<n;i++) {
            while(r<n && v.find(s[r])==v.end()){
                v.insert(s[r]);
                r++;
            }
            ans = max(ans, r - i);
            v.erase(s[i]);
        }
        return ans;
    }
};
```

> 2025年6月9日
```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int ans = 0;
        int n = s.length();
        set<char> v;
        int right = 0;
        for(int i=0;i<n;i++){
            while(v.find(s[right])==v.end() && right<n){
                v.insert(s[right]);
                right++;
            }
            if(right - i > ans){
                ans = right - i;
            }
            v.erase(s[i]);
        }
        return ans;
    }
};
```