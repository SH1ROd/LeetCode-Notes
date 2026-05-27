[字符串排序_牛客题霸_牛客网](https://www.nowcoder.com/practice/5af18ba2eb45443aa91a11e848aa6723?tpId=37&tqId=21237&rp=1&sourceUrl=%2Fexam%2Foj%2Fta%3FtpId%3D37&difficulty=undefined&judgeStatus=undefined&tags=&title=)
```python
n = int(input())
v = []
for i in range(n):
    a = input()
    v.append(a)
v.sort()
for s in v:
    print(s)
```