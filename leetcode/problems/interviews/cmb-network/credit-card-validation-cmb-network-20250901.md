**题目：信用卡合法性验证**

请实现一个信用卡号码合法性验证的方法。验证规则如下：

1. **基本要求**：
   - 卡号长度必须为15-19位
   - 只能包含数字字符（0-9），不允许其他字符

2. **Luhn算法验证**：
   - 从右往左，对每一位数字进行处理
   - 对于偶数位（从右往左数，最右边为第1位），将该数字乘以2
   - 如果乘积是两位数（大于9），则将两位数字相加（如16→1+6=7）
   - 将所有数字（包括未处理和处理后的）相加得到总和
   - 如果总和能被10整除，则卡号合法

请完成以下代码框架：

```java
import java.util.Scanner;

public class CreditCardValidation {
    
    public static boolean isValidCardNumber(String cardNumber) {
        // 在此实现验证逻辑
        // 步骤1：检查卡号是否为null
        // 步骤2：检查长度是否为15-19位
        // 步骤3：检查是否只包含数字
        // 步骤4：实现Luhn算法验证
        // 步骤5：返回最终验证结果
        
        return false;
    }
    
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String inputCardNumber = scanner.nextLine();
        scanner.close();
        
        boolean isValid = isValidCardNumber(inputCardNumber);
        System.out.println(isValid);
    }
}
```

## 测试用例

请使用以下测试用例验证你的实现：

1. **合法卡号**：长度16位、全数字、通过Luhn算法验证
2. **非法卡号**：包含非数字字符
3. **非法卡号**：长度13位（不符合15-19位要求）
4. **非法卡号**：长度16位但未通过Luhn算法验证
5. **合法卡号**：长度18位、全数字、通过Luhn算法验证

请根据上述要求完成 `isValidCardNumber` 方法的实现。

## **解析**

### 1. 基本规则检查

* **长度检查**：卡号长度必须在 15–19 位之间。
* **数字检查**：卡号只能包含数字字符（0-9），其他字符直接判定非法。
* **空值检查**：防止 `null` 导致异常。

### 2. Luhn 算法

* 从右向左处理每一位数字。
* 对于偶数位（从右边开始数，最右边为第 1 位），将数字乘以 2。
* 如果乘积大于 9，则将其拆分后相加（或者直接减 9，也是一种简化方法）。
* 将所有数字求和。
* 总和能被 10 整除即合法。

---

### **Java 实现**

```java
import java.util.Scanner;

public class CreditCardValidation {

    public static boolean isValidCardNumber(String cardNumber) {
        // 步骤1：检查是否为null
        if (cardNumber == null) {
            return false;
        }

        // 步骤2：检查长度
        int length = cardNumber.length();
        if (length < 15 || length > 19) {
            return false;
        }

        // 步骤3：检查是否只包含数字
        if (!cardNumber.matches("\\d+")) { // 正则匹配数字
            return false;
        }

        // 步骤4：实现Luhn算法
        int sum = 0;
        boolean doubleDigit = false; // 从右向左，偶数位标记

        for (int i = length - 1; i >= 0; i--) {
            int digit = cardNumber.charAt(i) - '0';
            if (doubleDigit) {
                digit *= 2;
                if (digit > 9) {
                    digit -= 9; // 两位数拆分相加的简便方法
                }
            }
            sum += digit;
            doubleDigit = !doubleDigit; // 翻转偶数位标记
        }

        // 步骤5：返回最终验证结果
        return sum % 10 == 0;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("请输入信用卡号：");
        String inputCardNumber = scanner.nextLine();
        scanner.close();

        boolean isValid = isValidCardNumber(inputCardNumber);
        System.out.println(isValid);
    }
}
```

---

### **测试用例验证**

| 测试用例 | 输入示例                             | 预期输出    |
| ---- | -------------------------------- | ------- |
| 合法卡号 | `4539578763621486` (16位，Luhn通过)  | `true`  |
| 非法卡号 | `4539a78763621486` (包含字母)        | `false` |
| 非法卡号 | `1234567890123` (长度13)           | `false` |
| 非法卡号 | `4539578763621487` (16位，但Luhn失败) | `false` |
| 合法卡号 | `6011000990139424` (18位，Luhn通过)  | `true`  |

---

### **重点说明**

1. `doubleDigit` 标记用于控制“偶数位乘2”的逻辑，从右往左循环。
2. `digit > 9` 时 `digit -= 9` 是 Luhn 的简化计算（等价于拆分各位数字再相加）。
3. `cardNumber.matches("\\d+")` 是检查全数字的最简单方法。
4. 方法返回值为布尔型，方便直接在 `main` 打印验证结果。