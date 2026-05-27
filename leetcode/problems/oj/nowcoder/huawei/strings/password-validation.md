#字符串 #模拟 
[密码验证合格程序_牛客题霸_牛客网](https://www.nowcoder.com/practice/184edec193864f0985ad2684fbc86841?tpId=37&rp=1&sourceUrl=%2Fexam%2Foj%2Fta%3FtpId%3D37&difficulty=&judgeStatus=&tags=&title=&gioEnter=menu)
```python
import sys

def check(s):
    if len(s) <= 8:
        return 0
    a,b,c,d = 0, 0, 0, 0
    for t in line:
        if str(t).isupper():
            a=1
        elif str(t).islower():
            b=1
        elif str(t).isdigit():
            c=1
        elif t!='\n':
            # print(t)
            d=1
    # print(a, b, c, d)
    if a+b+c+d < 3:
        return 0

    # v = set()
    # for i in range(len(s) - 2):
    #     if s[i:i+3] in v:
    #         return 0
    #     else:
    #         v.add(s[i:i+3])
    # return 1

    for i in range(len(s) - 2):
        if len(s.split(s[i:i+3])) >= 3:
            return 0
    return 1
    
for line in sys.stdin:
    if check(line):
        print("OK")
    else:
        print("NG")



```

>标准答案和我的区别
```python
	# 我的答案
	# v = set()
    # for i in range(len(s) - 2):
    #     if s[i:i+3] in v:
    #         return 0
    #     else:
    #         v.add(s[i:i+3])
    # return 1
	
	# 官方题解
    for i in range(len(s) - 2):
        if len(s.split(s[i:i+3])) >= 3:
            return 0
    return 1```

### 简短笔记：独立子串的区别及算法判别

#### **独立子串与非独立子串：**

* **独立子串**：两个子串 **完全不同的位置**，且没有任何重叠部分。
* **非独立子串**：两个子串 **有重叠部分**，即它们共享部分字符。

#### **例子：**

* **合法的例子**：

  * `"1111"`：包含 `"11"` 和 `"11"`，但它们 **重叠**，所以不是独立子串，合法。
* **不合法的例子**：

  * `"abcabc"`：包含两个独立的 `"abc"`，所以是 **不合法**。

#### **两种算法的判别差异：**

1. **基于 `set()` 存储子串（你的代码）**：

   * 通过遍历所有长度为 3 的子串，并将其加入集合 `v`。
   * 如果当前子串已经在集合中，说明该子串重复，直接返回 `0`。
   * **关键点**：只关注子串是否出现过，不考虑它们是否独立。如果两个子串有重叠，仍然算作重复。

   **优点**：高效，时间复杂度为 O(n)，适用于大多数情况。

   **缺点**：无法处理子串有重叠但不独立的情况。比如 `"1111"` 被判定为合法，而 `"abcabc"` 被判定为不合法。

2. **基于 `split()` 判断重复（答案的代码）**：

   * 使用 `split()` 方法将字符串按照当前子串分割。如果分割后的字符串部分多于 2 个，说明该子串出现了 3 次或更多。
   * **关键点**：这种方法实际上检查子串是否出现在字符串中多次，如果子串有重叠部分，`split()` 也会把它视为一次出现。

   **优点**：简洁，适用于检查子串出现次数。

   **缺点**：性能上稍逊色，尤其是当子串重复的次数较多时。并且这种方法可能无法准确判断子串是否独立。

#### **总结：**

* **你的代码** 使用 `set()` 来检查重复子串，但不会判断子串是否独立，适用于大部分情况下的子串检测。
* **答案的代码** 使用 `split()` 来判断子串的重复出现次数，虽然简单，但也可能不能完全解决子串的重叠问题。
