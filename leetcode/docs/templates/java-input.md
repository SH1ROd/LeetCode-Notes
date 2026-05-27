# Java 输入处理模板汇总

Java 做题常用输入方式主要有两种：**Scanner** 和 **BufferedReader + StringTokenizer**。下面按类型总结：

---

## 1. 读取单行字符串

```java
import java.util.Scanner;

Scanner sc = new Scanner(System.in);
String line = sc.nextLine(); // 整行输入
````

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;

BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
String line = br.readLine(); // 整行输入
```

---

## 2. 读取单个整数 / 多个整数

### 单个整数

```java
int n = sc.nextInt();
```

### 多个整数（同一行空格分隔）

```java
String[] parts = sc.nextLine().split(" ");
int[] nums = new int[parts.length];
for(int i = 0; i < parts.length; i++){
    nums[i] = Integer.parseInt(parts[i]);
}
```

或者使用 BufferedReader + StringTokenizer：

```java
String line = br.readLine();
StringTokenizer st = new StringTokenizer(line);
int[] nums = new int[st.countTokens()];
for(int i = 0; st.hasMoreTokens(); i++){
    nums[i] = Integer.parseInt(st.nextToken());
}
```

---

## 3. 读取字符列表 / 字符串数组

```java
String line = sc.nextLine();
String[] words = line.split(" "); // 按空格分隔
```

---

## 4. 按规则处理特殊结束符（如 # 结束）

```java
String line = sc.nextLine();
line = line.substring(0, line.length() - 1); // 去掉结尾 #
String[] words = line.split(" ");
```

---

## 5. 多行输入（行数未知，可用 while 循环）

```java
while(sc.hasNextLine()){
    String line = sc.nextLine();
    // 处理 line
}
```

---

## 6. 高性能输入（大数据量时推荐）

```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
int n = Integer.parseInt(br.readLine());
```

> **总结**：
>
> * 小数据量 → Scanner 足够
> * 大数据量 → BufferedReader + StringTokenizer
> * 按空格分隔 → `split(" ")` 或 StringTokenizer
> * 按行结束符 → `readLine()`
> * 结尾特殊符 → `substring()` 去掉