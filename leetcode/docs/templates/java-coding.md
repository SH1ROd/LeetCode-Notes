```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        // ======================
        // 输入部分
        // ======================
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st;

        // -------- 单行字符串输入 --------
        String line = br.readLine();  // 整行字符串
        // 如果有特殊结束符，比如 #
        if(line.endsWith("#")) {
            line = line.substring(0, line.length() - 1);
        }
        String[] words = line.split(" "); // 按空格分割字符串数组

        // -------- 单个整数输入 --------
        int n = Integer.parseInt(br.readLine());

        // -------- 多个整数输入（同一行空格分隔） --------
        st = new StringTokenizer(br.readLine());
        int m = st.countTokens();
        int[] nums = new int[m];
        for(int i = 0; st.hasMoreTokens(); i++){
            nums[i] = Integer.parseInt(st.nextToken());
        }

        // -------- 多行输入（行数未知） --------
        /*
        String s;
        while((s = br.readLine()) != null && !s.isEmpty()){
            // 处理每行 s
        }
        */

        // ======================
        // 处理逻辑部分
        // ======================
        // 在这里写你的算法逻辑

        // ======================
        // 输出部分
        // ======================
        // 输出单行字符串
        System.out.println(String.join(" ", words));

        // 输出数组
        // for(int x : nums){
        //     System.out.print(x + " ");
        // }
        // System.out.println();
    }
}

```