#动态规划 #背包问题
**题目整理：**

这是一个典型的 **0-1背包问题**。  

**问题描述：**  
- 给定报销额度（背包容量）`C` 和菜品数量 `N`。  
- 每种菜品有价格 `P`（相当于物品重量）和评价分数 `W`（相当于物品价值）。  
- 目标：在不超过报销额度的情况下，选择菜品（每种最多选一次），使得总评价分数最大。  

**输入格式：**  
- 第一行：`C N`  
- 接下来 `N` 行：每行两个整数 `P W`（价格和评价分数）  

**输出格式：**  
- 一个整数：最大评价分数  

**示例：**  
输入1：  
```
90 4
20 25
30 30
40 40
10 10
8 8
9 9
5 5
```
输出1：  
```
95
```

输入2：  
```
40 4
25 10
8 9
5 8
9 5
```
输出2：  
```
38
```

**标签类别：**  
- **动态规划（Dynamic Programming）**  
- **0-1背包问题（0-1 Knapsack Problem）**

>答案

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        // 读取总报销额度 C 和菜品数量 N
        int C = scanner.nextInt();
        int N = scanner.nextInt();
        
        int[] prices = new int[N];
        int[] scores = new int[N];
        
        for (int i = 0; i < N; i++) {
            prices[i] = scanner.nextInt();
            scores[i] = scanner.nextInt();
        }
        
        // dp[j] 表示报销额度为 j 时能获得的最大评价分数
        int[] dp = new int[C + 1];
        
        // 遍历每个菜品
        for (int i = 0; i < N; i++) {
            // 反向遍历，避免重复选择
            for (int j = C; j >= prices[i]; j--) {
                dp[j] = Math.max(dp[j], dp[j - prices[i]] + scores[i]);
            }
        }
        
        // 输出最大评价分数
        System.out.println(dp[C]);
        
        scanner.close();
    }
}
```