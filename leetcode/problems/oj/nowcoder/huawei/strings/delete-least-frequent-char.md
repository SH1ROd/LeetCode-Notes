#字符串
[删除字符串中出现次数最少的字符_牛客题霸_牛客网](https://www.nowcoder.com/practice/05182d328eb848dda7fdd5e029a56da9?tpId=37&rp=1&sourceUrl=%2Fexam%2Foj%2Fta%3FtpId%3D37&difficulty=&judgeStatus=&tags=&title=&gioEnter=menu)
```python
s=input()
d = {}
for t in s:
    d[t]=d.get(t,0)+1 
sorted_item = sorted(d.items(), key=lambda x:x[1], reverse=True)
del_chars = []
first = sorted_item.pop()
num = first[1]
del_chars.append(first[0])

# while (a=sorted_item.pop()) and a[1]==num:
#     del_chars.append(a[0])
while sorted_item:
    a=sorted_item.pop()
    if a[1]==num:
        del_chars.append(a[0])
    else:
        break
ans = list(s)
for p in del_chars:
    while p in ans:
        ans.remove(p)
print(''.join(ans))

```

> 字典按value排序, 使用`key=lambda x:x[1]`, 逆序`reverse=True`
```python
sorted_item = sorted(d.items(), key=lambda x:x[1], reverse=True)
```

> 删除全部指定字符
```python
while p in ans:
	ans.remove(p)
```


>题解
```python
while True:
    try:
        s = input()
        dic, res = {}, ''
        for c in s:
            if c not in dic:
                dic[c] = 1
            else:
                dic[c] += 1
        Min = min(dic.values())
        for c in s:
            if dic[c] != Min:
                res += c
        print(res)
    except:
        break

```

>可以直接使用 `min(d.values())` 找到最小值


>GPT优化版: 
```python
s = input()
d = {}
# 统计字符出现次数
for t in s:
    d[t] = d.get(t, 0) + 1
    
# 找到最少出现次数
min_count = min(d.values())

# 将出现次数最少的字符放入一个集合
del_chars = {k for k, v in d.items() if v == min_count}

# 构造结果字符串，去除掉出现次数最少的字符
res = ''.join([c for c in s if c not in del_chars])

print(res)

```

> 列表推导式用法: 
> `{k for k, v in d.items() if v == min_count}`
> `[c for c in s if c not in del_chars]`
> 一般来说，如果你在写 `for` 循环时，
> 意识到循环体内是**为了生成一个新的列表**，
> 或者是基于某些条件**过滤掉不需要的元素**，
> 这时就可以考虑使用列表推导式。