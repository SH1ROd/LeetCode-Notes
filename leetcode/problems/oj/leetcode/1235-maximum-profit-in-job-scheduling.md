#动态规划 #区间调度 
[1235. 规划兼职工作 - 力扣（LeetCode）](https://leetcode.cn/problems/maximum-profit-in-job-scheduling/description/)

> 空开数组的第一格

```c++
class Solution {
struct job{
    int startTime;
    int endTime;
    int profit;
};
public:
    int jobScheduling(vector<int>& startTime, vector<int>& endTime, vector<int>& profit) {
        int n = startTime.size();
        vector<job> v(n+1);
        for (int i=1;i <= n;i++){
            v[i].startTime = startTime[i-1];
            v[i].endTime = endTime[i-1];
            v[i].profit = profit[i-1];
        }
        sort(v.begin() + 1, v.end(), [](const job &a, const job &b){
            return a.endTime<b.endTime;
        });
        vector<int> ends(n+1, 0);
        for (int i=1;i<=n;i++){
            ends[i] = v[i].endTime;
        }
        vector<int> pre(n+1, 0);
        for (int i=1;i<=n;i++) {
            int index = upper_bound(ends.begin()+ 1, ends.begin() + i, v[i].startTime)-ends.begin() -1;
            pre[i] = index;
        }
        vector<int> dp(n+1, 0);
        for (int i=1;i<=n;i++) {
            dp[i] = max(dp[i-1], dp[pre[i]] + v[i].profit);
        }
        return dp[n];
    }

};
```

> 不空开数组的第一格

```c++
class Solution {
public:
    struct job{
        int startTime;
        int endTime;
        int profit;
    };
    int jobScheduling(vector<int>& startTime, vector<int>& endTime, vector<int>& profit) {
      int n = startTime.size();
      vector<job> v(n);
      for(int i=0;i<n;i++){
        v[i].startTime = startTime[i];
        v[i].endTime = endTime[i];
        v[i].profit = profit[i];
      }
      sort(v.begin(), v.end(), [](job &a, job &b){
        return a.endTime < b.endTime;
      });

      vector<int> endTimeSort(n, 0);
      for(int i=0;i<n;i++){
        endTimeSort[i] = v[i].endTime;
        cout << "endTimeSort: " << endTimeSort[i] << endl;
      }

      vector<int> pre(n);
      for(int i=0;i<n;i++){
        pre[i] = upper_bound(endTimeSort.begin(), endTimeSort.begin()+ i, v[i].startTime) - endTimeSort.begin() - 1;
        cout << "startTime: " << v[i].startTime << endl;
        cout << "profit: " << v[i].profit << endl;
        cout << "pre: " <<  pre[i] << endl;
      }

    vector<int> dp(n+1, 0);
    dp[0] = v[0].profit;
    for(int i=1;i<n;i++){
        if(pre[i]==-1){
            dp[i] = max(dp[i-1], v[i].profit);
        }
        else{
            dp[i] = max(dp[i-1], dp[pre[i]] + v[i].profit);
        }
    }
      return dp[n-1];  
    }
};
```

>Python第一版
```python
class Solution:
    def jobScheduling(self, startTime: List[int], endTime: List[int], profit: List[int]) -> int:
        events = [[x, y, z] for x, y, z in zip(startTime, endTime, profit)]
        n = len(events)
        events.sort(key = lambda e:e[1])
        ends = [0] + [x[1] for x in events]
        pre = [0] * (n + 1)
        for i in range(1, n + 1):
            pre[i] = bisect_right(ends, events[i - 1][0]) - 1
        dp = [0] * (n + 1)
        for i in range(1, n + 1):
            dp[i] = max(dp[i - 1], dp[pre[i]] + events[i - 1][2])
        return dp[n]
```

>下一版
```python

```