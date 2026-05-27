好的，我们来系统梳理一下 **Java Stream 的中间操作**。中间操作的特点是 **返回一个新的 Stream，可以链式调用**，不会触发流的遍历，只有终端操作才会真正执行。它们主要用于 **转换、过滤、排序、映射** 等操作。

---

## 1. 分类概览

### （1）**筛选（Filtering）**

- 用于过滤流中的元素，返回符合条件的子流
    
- 常用方法：
    
    - `filter(Predicate<? super T> predicate)`：根据条件筛选
        
    - `distinct()`：去重，依赖 `hashCode()` 和 `equals()`
        
- 示例：
    

```java
Stream.of(1,2,2,3,4)
      .filter(n -> n % 2 == 0)  // 筛选偶数
      .distinct()               // 去重
      .forEach(System.out::println);
```

---

### （2）**映射（Mapping）**

- 将元素转换成另一种形式
    
- 常用方法：
    
    - `map(Function<? super T, ? extends R> mapper)`：一对一映射
        
    - `flatMap(Function<? super T, ? extends Stream<? extends R>> mapper)`：一对多映射，把嵌套 Stream 展平
        
    - `mapToInt`, `mapToLong`, `mapToDouble`：映射到基本类型流
        
- 示例：
    

```java
Stream.of("a", "bb", "ccc")
      .map(String::length) // 变成长度
      .forEach(System.out::println);

Stream.of(Arrays.asList(1,2), Arrays.asList(3,4))
      .flatMap(List::stream)
      .forEach(System.out::println);
```

---

### （3）**切片（Slicing）**

- 对流进行截取或跳过
    
- 常用方法：
    
    - `limit(long maxSize)`：截取前 N 个元素
        
    - `skip(long n)`：跳过前 N 个元素
        
- 示例：
    

```java
Stream.of(1,2,3,4,5)
      .skip(2)
      .limit(2)
      .forEach(System.out::println); // 输出 3,4
```

---

### （4）**排序（Sorting）**

- 对元素排序
    
- 常用方法：
    
    - `sorted()`：自然顺序（需实现 Comparable）
        
    - `sorted(Comparator<? super T> comparator)`：自定义顺序
        
- 示例：
    

```java
Stream.of(3,1,4,2)
      .sorted()
      .forEach(System.out::println); // 输出 1,2,3,4
```

---

### （5）**其他转换**

- **`peek(Consumer<? super T> action)`**
    
    - 用于调试或中间操作时查看元素
        
    - 返回新的 Stream
        
- **示例：**
    

```java
Stream.of(1,2,3)
      .peek(System.out::println)
      .map(n -> n * n)
      .forEach(System.out::println);
```

---

## 2. 流的延迟性

- 中间操作都是 **惰性执行** 的，不会马上处理数据。
    
- 只有遇到 **终端操作**（如 `collect`、`forEach`、`reduce`）时，整个流水线才会执行。
    
- 优点：可以合并操作，减少中间对象，效率更高。
    

---

## 3. 总结

|类别|方法举例|作用|
|---|---|---|
|筛选|`filter`, `distinct`|挑选元素、去重|
|映射|`map`, `flatMap`, `mapToInt`|元素转换|
|切片|`limit`, `skip`|截取或跳过部分元素|
|排序|`sorted`|排序流元素|
|调试/观察|`peek`|中间观察元素|

> 小技巧：中间操作可以无限链式组合，例如：

```java
Stream.of("a","bb","ccc")
      .filter(s -> s.length() > 1)
      .map(String::toUpperCase)
      .sorted()
      .forEach(System.out::println);
```

这个例子先筛选，再转换，再排序，最后输出。

---

如果你需要，我可以帮你画一个 **“Stream 中间操作 → 终端操作 → 结果容器” 的完整流程图**，让你一眼看到整个 Stream 的数据流动过程。

你希望我画吗？