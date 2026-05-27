给你一个**最简表格版**👇

---

## ✅ accumulate 语法总表

|项|写法|说明|
|---|---|---|
|基本语法|`accumulate(nums, f, initial=init)`|通用形式|
|函数 f|`lambda x, y: ...`|上一个结果 + 当前元素|
|含 initial|`res[0]=init`|从初始值开始|
|不含 initial|`res[0]=nums[0]`|从第一个元素开始|

---

## ✅ 执行逻辑

|写法|等价代码|
|---|---|
|有 initial|`res=[init]; for y in nums: res.append(f(res[-1], y))`|
|无 initial|`res=[nums[0]]; for i>0: res.append(f(res[-1], nums[i]))`|

---

## ✅ 常见用法

|功能|写法|initial|
|---|---|---|
|前缀和|`lambda x,y: x+y`|0|
|前缀积|`lambda x,y: x*y`|1|
|前缀异或|`lambda x,y: x^y`|0|
|前缀最大|`lambda x,y: max(x,y)`|一般不用|
|前缀最小|`lambda x,y: min(x,y)`|一般不用|

---

## ✅ 关键点

|点|说明|
|---|---|
|f 参数|必须是二元函数|
|initial|会让结果长度 +1|
|本质|滚动变量 / 一维DP|

---

## ✅ 一句话

👉 `accumulate = 用函数 f 把序列“滚动累积”起来`