[合并表记录_牛客题霸_牛客网](https://www.nowcoder.com/practice/de044e89123f4a7482bd2b214a685201?tpId=37&tqId=21231&rp=1&sourceUrl=%2Fexam%2Foj%2Fta%3FtpId%3D37&difficulty=undefined&judgeStatus=undefined&tags=&title=)

```python
n = int(input())  
d = {}  
for i in range(n):  
    k, v = map(int, input().split())  
    d[k] = d.get(k, 0) + v  
sorted_items = sorted(d.items(), key=lambda x: x[0])  
for a in sorted_items:  
    print(str(a[0]) + " " + str(a[1]))
```