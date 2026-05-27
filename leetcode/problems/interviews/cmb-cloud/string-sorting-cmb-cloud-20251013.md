# B卷编程题（20分）

- 每题以多次提交中最高得分计分  
- 时间限制：1秒  
- 空间限制：262MB  
- 限定语言：Java（javac 1.8）  
- 64bit IO 格式：`%lld`  
- 本题可使用本地 IDE 编码，但不能使用本地已有代码  
- 编码后请点击“保存并提交”按钮进行提交  

## 题目描述
给定一个字符列表（字符串仅由小写英文字母组成），请按照以下规则对列表项进行排序并输出：

1. **主要规则**：按照字符串长度降序排列（长度长的在前）  
2. **次要规则**：当字符串长度相同时，按照字符串的逆序进行字典序升序排列  
   - 例如 `"abxe"` 的逆序为 `"exba"`，比较时使用逆序后的字符串  

## 输入描述
- 输入为单行字符串，以 `#` 结尾  
- 字符串间用 1 个空格分隔  
- 保证输入中无空字符串  

## 输出描述
- 排序后的字符串列表，用单个空格分隔  
- 结尾无空格

## 输入输出示例

### 示例 1
**输入：**
```

apple bat cat dog elephant#

```
**输出：**
```

elephant apple dog bat cat

```

### 示例 2
**输入：**
```

abc xyz a ab#

```
**输出：**
```

abc xyz ab a

```

### 示例 3
**输入：**
```

hello#

```
**输出：**
```

hello

```

### 示例 4
**输入：**
```

dog god cat tac bat tab#

```
**输出：**
```

god dog tab bat tac cat

```

>个人写法
```java
import java.util.Arrays;
import java.util.Scanner;
import java.util.SimpleTimeZone;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String line = sc.nextLine();
        
        String[] s = line.substring(0, line.length() - 1).split(" ");
        
        String[] ans = Arrays
                .stream(s)
                .sorted((a, b) -> {
                    if (a.length() != b.length()) return b.length() - a.length();
                    return new StringBuilder(a)
                            .reverse().toString()
                            .compareTo(new StringBuilder(b).reverse().toString());
                })
                .toArray(String[]::new);
                
        System.out.println(String.join(" ", ans));
    }
}

```

>多种写法
```java
import java.util.Arrays;
import java.util.Scanner;
import java.util.SimpleTimeZone;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String line = sc.nextLine();

//        去除最后一个字符
        String[] s = line.substring(0, line.length() - 1).split(" ");

////        正则表达式匹配
//        String[] s = line.replaceAll("^#+|#+$", "").split(" ");

//        转stream后修改再转回数组
        String[] ans = Arrays
                .stream(s)
                .sorted((a, b) -> {
                    if (a.length() != b.length()) return b.length() - a.length();
                    return new StringBuilder(a)
                            .reverse().toString()
                            .compareTo(new StringBuilder(b).reverse().toString());
                })
                .toArray(String[]::new);

////        原地修改
//        Arrays.sort(s, (a, b) -> {
//            if (a.length() != b.length()) return b.length() - a.length();
//            return new StringBuilder(a)
//                    .reverse().toString()
//                    .compareTo(new StringBuilder(b).reverse().toString());
//            });
//        String[] ans = s;

//        join输出
        System.out.println(String.join(" ", ans));

////        循环输出
//        System.out.print(ans[0]);
//        for (int i=1;i<ans.length;i++){
//            System.out.print(" " + ans[i]);
//        }
    }
}

```