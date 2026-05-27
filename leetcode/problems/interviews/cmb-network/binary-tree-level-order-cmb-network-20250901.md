#二叉树 #BFS #队列
**题目：二叉树层次遍历**

## 题目内容

编写一个方法levelOrderTraversal，对二叉树进行层次遍历（广度优先搜索、从左到右），并输出遍历结果。请补全下面程序中块【】位置缺失的代码，以实现该功能。

```java
import java.util.Queue;
import java.util.LinkedList;
import java.util.Set;
import java.util.HashSet;

// 定义二叉树节点类
class TreeNode {
    int val;
    TreeNode left; // 左子节点
    TreeNode right; // 右子节点
    // 构造方法，初始化节点值
    TreeNode(int x) {
        val = x;
    }
}

public class LevelOrderTraversal {
    // 层次遍历方法，参数为二叉树的根节点
    public static void levelOrderTraversal(TreeNode root) {
        // 如果根节点为null，直接返回（无需遍历）
        if (root == null) {
            return;
        }
        // 初始化队列，用于存储待处理的节点
        Queue<TreeNode> queue = new LinkedList<>();
        // 初始化集合，用于标记访问过的节点
        Set<TreeNode> visited = new HashSet<>();
        // 根节点加入队列和已访问集合
        queue.add(root);
        visited.add(root);

        // 当队列不为空时，循环处理节点
        while (!queue.isEmpty()) {
            // 从队列中取出当前节点
            TreeNode current = queue.poll();
            // 输出当前节点的值
            System.out.print(current.val + " ");

            // 处理左子节点，若左子节点不为null且未被访问，加入队列和已访问集合
            if (【】 != null && !visited.contains(【】)) {
                queue.add(【】);
                visited.add(【】);
            }
            // 处理右子节点，若右子节点不为null且未被访问，加入队列和已访问集合
            if (【】 != null && !visited.contains(【】)) {
                queue.add(【】);
                visited.add(【】);
            }
        }
    }

    // 主方法，用于测试层次遍历功能
    public static void main(String[] args) {
        // 创建二叉树结构：
        //     1
        //    / \
        //   2   3
        //  / \
        // 4   5
        TreeNode root = new TreeNode(1); // 根节点
        root.left = new TreeNode(2); // 根节点的左子节点
        root.right = new TreeNode(3); // 根节点的右子节点
        root.left.left = new TreeNode(4); // 左子节点的左子节点
        root.left.right = new TreeNode(5); // 左子节点的右子节点
        
        // 输出提示信息
        System.out.print("层次遍历结果: ");
        // 调用层次遍历方法
        levelOrderTraversal(root);
    }
}
```

## 测试样例说明

构造的二叉树共5个节点，层次遍历按照"根节点-第一层（左、右子节点）-第二层（左子节点的子节点）"的顺序访问，即先访问根节点1，再访问第一层的2和3，最后访问第二层的4和5，最终输出"1 2 3 4 5"。

## **题目解析**

### 1. 层次遍历思路

* 层次遍历（BFS，广度优先搜索）通常使用 **队列（Queue）** 来实现。
* 步骤：

  1. 将根节点加入队列。
  2. 当队列不为空时：

     * 取出队首节点 `current`。
     * 访问节点（这里是打印 `current.val`）。
     * 如果左子节点存在且未访问，加入队列。
     * 如果右子节点存在且未访问，加入队列。
* **访问标记**：用 `Set<TreeNode>` 保存已经访问过的节点，防止重复访问。

### 2. 队列和访问集合逻辑

* 左子节点检查：

  ```java
  if (current.left != null && !visited.contains(current.left)) {
      queue.add(current.left);
      visited.add(current.left);
  }
  ```
* 右子节点检查：

  ```java
  if (current.right != null && !visited.contains(current.right)) {
      queue.add(current.right);
      visited.add(current.right);
  }
  ```

> 注意：这里的 `current` 是队首节点，左子节点为 `current.left`，右子节点为 `current.right`。

---

### **缺失代码补全**

将原代码中的 `【】` 替换为对应表达式：

```java
// 处理左子节点
if (current.left != null && !visited.contains(current.left)) {
    queue.add(current.left);
    visited.add(current.left);
}

// 处理右子节点
if (current.right != null && !visited.contains(current.right)) {
    queue.add(current.right);
    visited.add(current.right);
}
```

---

### **完整方法**

```java
public static void levelOrderTraversal(TreeNode root) {
    if (root == null) {
        return;
    }
    Queue<TreeNode> queue = new LinkedList<>();
    Set<TreeNode> visited = new HashSet<>();
    queue.add(root);
    visited.add(root);

    while (!queue.isEmpty()) {
        TreeNode current = queue.poll();
        System.out.print(current.val + " ");

        if (current.left != null && !visited.contains(current.left)) {
            queue.add(current.left);
            visited.add(current.left);
        }
        if (current.right != null && !visited.contains(current.right)) {
            queue.add(current.right);
            visited.add(current.right);
        }
    }
}
```

---

### **输出结果验证**

给定二叉树：

```
    1
   / \
  2   3
 / \
4   5
```

* 遍历顺序：

  1. 根节点：`1`
  2. 第一层：`2`、`3`
  3. 第二层：`4`、`5`

* 输出：

```
层次遍历结果: 1 2 3 4 5
```

---

### **小结**

1. 层次遍历核心在于 **队列**。
2. 左右子节点依次入队，保证从左到右顺序。
3. 使用 `visited` 可以避免图结构中重复访问（在二叉树中可省略，因为没有环，但题目给了Set，也可以保留）。
4. BFS 时间复杂度为 **O(n)**，空间复杂度为 **O(n)**（队列可能存储一层所有节点）。
