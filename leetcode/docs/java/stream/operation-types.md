明白了，你想对 **Java Stream 的处理方式**有一个简单、实用的概览，同时配例子。我帮你整理成易理解的表格和示例。

---

## 1️⃣ Stream 的三类操作

Java Stream 操作可以分为三类：

| 类别                     | 作用           | 方法举例                                              | 说明                  |
| ---------------------- | ------------ | ------------------------------------------------- | ------------------- |
| **创建 Stream**          | 从集合、数组等创建流   | `stream()`, `of()`, `Arrays.stream()`             | 用于生成 Stream 对象      |
| **中间操作（Intermediate）** | 对元素做加工、转换、过滤 | `filter()`, `map()`, `sorted()`, `distinct()`     | 返回一个新的 Stream，可链式调用 |
| **终端操作（Terminal）**     | 获取结果或输出      | `collect()`, `forEach()`, `toArray()`, `reduce()` | 执行 Stream 流程，结束链式调用 |

---

## 2️⃣ 常见中间操作举例

### （1）`map` — 映射元素

```java
List<String> list = Arrays.asList("a","bb","ccc");
List<Integer> lengths = list.stream()
                            .map(String::length)
                            .collect(Collectors.toList());
System.out.println(lengths); // 输出 [1, 2, 3]
```

---

### （2）`filter` — 过滤元素

```java
List<String> list = Arrays.asList("apple","bat","cat");
List<String> longWords = list.stream()
                             .filter(s -> s.length() > 3)
                             .collect(Collectors.toList());
System.out.println(longWords); // 输出 [apple]
```

---

### （3）`sorted` — 排序

```java
String[] arr = {"dog", "apple", "cat"};
String[] sorted = Arrays.stream(arr)
                        .sorted()
                        .toArray(String[]::new);
System.out.println(Arrays.toString(sorted)); // 输出 [apple, cat, dog]
```

* 自定义排序：

```java
Arrays.stream(arr)
      .sorted((a,b) -> b.length() - a.length()) // 长度降序
      .toArray(String[]::new);
```

---

### （4）`distinct` — 去重

```java
List<Integer> nums = Arrays.asList(1,2,2,3,3,3);
List<Integer> unique = nums.stream()
                           .distinct()
                           .collect(Collectors.toList());
System.out.println(unique); // 输出 [1, 2, 3]
```

---

## 3️⃣ 常见终端操作举例

| 方法        | 作用    | 例子                                                                  |
| --------- | ----- | ------------------------------------------------------------------- |
| `forEach` | 遍历元素  | `list.stream().forEach(System.out::println);`                       |
| `toArray` | 转数组   | `String[] arr = list.stream().toArray(String[]::new);`              |
| `collect` | 收集为集合 | `List<String> result = list.stream().collect(Collectors.toList());` |
| `reduce`  | 聚合    | `int sum = nums.stream().reduce(0, Integer::sum);`                  |

---

## 4️⃣ 链式操作示例

```java
List<String> list = Arrays.asList("apple","bat","cat","dog");
List<String> result = list.stream()
                          .filter(s -> s.length() > 2)       // 长度>2
                          .map(String::toUpperCase)          // 转大写
                          .sorted()                          // 字典序排序
                          .collect(Collectors.toList());

System.out.println(result); // 输出 [APPLE, BAT, CAT, DOG]
```

✅ 特点：**可以链式操作，中间操作不会立即执行，只有终端操作才触发计算**

---

如果你愿意，我可以帮你做一张 **Stream 常用方法速查表 + 输入输出示例**，把 **创建 → 中间 → 终端** 的流程和用法画成一页 Cheat Sheet，刷题直接看就懂。

你希望我做吗？
