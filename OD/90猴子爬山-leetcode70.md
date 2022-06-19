# 猴子爬山

一天一只顽猴想去从山脚爬到山顶，途中经过一个有个N个台阶的阶梯，但是这猴子有一个习惯： 每一次只能跳1步或跳3步，试问猴子通过这个阶梯有多少种不同的跳跃方式？

 **输入描述:**

- 输入只有一个整数N（0<N<=50）此阶梯有多少个阶梯

**输出描述:**

- 输出有多少种跳跃方式（解决方案数）


**示例1：**

```
输入
50

输出
122106097
```

**示例2：**

```
输入
3

输出
2
```

```java
package com.stanlong.leetcode;

import java.util.Scanner;

/**
 * 猴子爬山
 */
public class LeetCode {

    public static void main(String[] args) throws Exception {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] dp = new int[n+7];
        dp[0] = 1;
        for (int i = 0; i <= n; i++) {
            dp[i + 1] += dp[i];
            dp[i + 3] += dp[i];
        }
        System.out.println(dp[n]);
    }
}
```

```java
package com.stanlong.leetcode;

import java.util.Scanner;

/**
 * 猴子爬山
 * 采用动态规划
 * 状态转移方程为： dp[n] = dp[n-1] + dp[n-3]
 * 确定初始状态：
 * n=1时，只有一种跳法
 * n=2时，也只有一种
 * n=3时，就有两种跳法，一级一级跳或者一下跳到第三级
 */
public class LeetCode {

    public static void main(String[] args) throws Exception {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        if(n<3){
            System.out.println(1);
            return;
        }
        int[] dp = new int[n+1];
        dp[0] = 1;
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i < n; i++) {
            dp[i] = dp[i-1] + dp[i-3];
        }
        System.out.println(dp[n-1]);
    }
}
```

