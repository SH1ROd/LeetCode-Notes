#字符串 #模拟
[坐标移动_牛客题霸_牛客网](https://www.nowcoder.com/practice/119bcca3befb405fbe58abe9c532eb29?tpId=37&rp=1&sourceUrl=%2Fexam%2Foj%2Fta%3FtpId%3D37&difficulty=&judgeStatus=&tags=&title=&gioEnter=menu)
```python
p = [0, 0]
directs = {
    'A': [-1, 0],
    'D': [1, 0],
    'W': [0, 1],
    'S': [0, -1]
}
line = input()
instructs = line.split(';')
for s in instructs:
    num = s[1:]
    if len(s) > 1 and s[0] in directs and num.isdigit():
        dist = int(s[1:])
        p[0] = p[0] + directs[s[0]][0] * dist
        p[1] = p[1] + directs[s[0]][1] * dist
print(str(p[0]) + "," + str(p[1]))
    
```

>切片(String和List)
```python
num = s[1:] # 从index=1到字符串最后
num = s[::-1] # 逆序
```

>字符串是否是数字
```python
num.isdigit()
```