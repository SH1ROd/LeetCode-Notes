**题目：Java继承与多态代码输出分析**

请分析以下代码，注意继承关系、构造器调用顺序和多态特性。回答程序运行后的控制台输出内容（共六个输出）。

```java
class Parent {
    static {
        System.out.println("Parent static block");
    }
    
    {
        System.out.println("Parent instance block");
    }
    
    int x = 30;
    
    public Parent() {
        metbody();
    }
    
    void metbody() {
        System.out.println("Parent metbody " + x);
    }
}

class Child extends Parent {
    static {
        System.out.println("Child static block");
    }
    
    {
        System.out.println("Child instance block");
    }
    
    int x = 30;
    
    public Child() {
        x = 30;
    }
    
    void metbody() {
        System.out.println("Child metbody " + x);
    }
}

public class Bind {
    public static void main(String[] args) {
        new Child().metbody();
    }
}
```

## 代码分析

### 1. 类加载阶段（Static block）

* 当 `Child` 类被加载时，会先加载 `Parent` 类（父类先于子类加载）。
* **静态块按继承顺序执行**：

  1. `Parent static block`
  2. `Child static block`

---

### 2. 创建对象阶段（new Child()）

* **对象创建顺序**：

  1. 父类实例块
  2. 父类构造器
  3. 子类实例块
  4. 子类构造器

* **注意：父类构造器中调用了 `metbody()`**，这是一个 **多态方法**，实际运行时会调用 **子类的 `metbody()`**，即使此时子类的实例块还没执行。

---

### 3. 父类构造器中 `metbody()` 的执行

* 子类的 `x` 还未初始化（Java 默认值为 0）。
* 所以第一次调用 `Child.metbody()` 输出：

  ```
  Child metbody 0
  ```

---

### 4. 父类实例块

* 在调用父类构造器之前，会先执行父类实例块：

  ```
  Parent instance block
  ```

> 实际执行顺序：父类实例块 → 父类构造器

* 然而要注意，父类构造器先执行实例块，实例块中没有修改 `x`，所以 x 在父类构造器调用时还是子类的默认值 0。

---

### 5. 子类实例块

* 执行子类实例块：

  ```
  Child instance block
  ```

---

### 6. 子类构造器

* 子类构造器给 `x = 30;`，此时 x 被赋值。

---

### 7. main 方法再次调用 `metbody()`

* 此时子类对象完全构造完成，x = 30
* 输出：

  ```
  Child metbody 30
  ```

---

### 综上，控制台输出顺序：

1. Parent static block
2. Child static block
3. Parent instance block
4. Child metbody 0
5. Child instance block
6. Child metbody 30

---

### ✅ 输出总结

```
Parent static block
Child static block
Parent instance block
Child metbody 0
Child instance block
Child metbody 30
```

---

### 解析小结

1. **静态块**：按继承顺序执行，类加载时执行一次。
2. **实例块**：父类实例块 → 父类构造器 → 子类实例块 → 子类构造器。
3. **多态方法调用**：父类构造器中调用的虚方法会调用子类重写的方法，但此时子类字段尚未初始化（默认值）。