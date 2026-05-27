[查找兄弟单词_牛客题霸_牛客网](https://www.nowcoder.com/practice/03ba8aeeef73400ca7a37a5f3370fe68?tpId=37&tqId=21250&rp=1&sourceUrl=%2Fexam%2Foj%2Fta%3FtpId%3D37&difficulty=undefined&judgeStatus=undefined&tags=&title=)
```python
parts = input().split()
n = int(parts[0])
v = []
for i in range(n):
    v.append(parts[i+1])
x = parts[-2]
k = int(parts[-1])
ans = []
for s in v:
    if s!=x and sorted(list(s))==sorted(list(x)):
        ans.append(s)
ans.sort()
print(len(ans))
if k-1>=0 and k-1 < len(ans):
    print(ans[k-1])
```