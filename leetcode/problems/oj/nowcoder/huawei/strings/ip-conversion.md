#字符串
[整数与IP地址间的转换_牛客题霸_牛客网](https://www.nowcoder.com/practice/66ca0e28f90c42a196afd78cc9c496ea?tpId=37&rp=1&sourceUrl=%2Fexam%2Foj%2Fta%3FtpId%3D37&difficulty=&judgeStatus=&tags=&title=&gioEnter=menu)

```python
# base = [2^(8*0), 2^(8*1), 2^(8*2), 2^(8*3)]
def ip2num(ip: str) -> int:
    parts = ip.split('.')
    return sum(int(x)*2**(8*i)  for i, x in enumerate(parts[::-1]))

def num2ip(num: int) -> str:
    ans = []
    while num>0:
        ans.append(num % 256)
        num //= 256
    return '.'.join(map(str, ans[::-1]))
    
a = input()
b = input()
print(ip2num(a))
print(num2ip(int(b)))
```

> **`num2ip` 函数中的 `while num > 0` 逻辑**：这个部分是有效的，但是它可能会遗漏一些边界情况，例如输入数字 `0` 时。实际上，`num2ip` 在处理 `0` 的时候，应该返回 `'0.0.0.0'`。你可以在 `while` 循环之前加上一个条件判断来处理这个特殊情况。 