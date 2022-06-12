# 最大矩阵和

给定一个二维整数矩阵，要在这个矩阵中选出一个子矩阵，使得这个子矩阵内所有的数字和尽量大，我们把这个子矩阵称为和最大矩阵，子矩阵的选取原则是原矩阵中一块连续的矩形区域，单独一行、单独一列、整个矩阵，都算子矩阵。

**输入：**

输入的第一行包含2个整数n,m(1<=n,m<=10),表示一个n行m列矩阵，下面有n行，每行m个整数，同一行中，每两个数字之间一个空格，最后一个数字后没有空格，所有数字的取值范围为[-1000,1000]

**输出：**

输出一行，一个数字，表示选出的和最大子矩阵内所有数字的和。

**样例：**

```
输入：
3 3
951 589 39
-583 -710 473
-229 501 -594
```

**输出**

```
1579
```

**解释：**

```java
最大子矩阵就是
951 589 39
求和得到1579
```

**解法一：**

前缀和

https://blog.csdn.net/yuhaomogui/article/details/123954619

```java
package com.stanlong.leetcode;

import java.io.BufferedInputStream;
import java.util.Scanner;

public class LeetCode {
    public static void main(String[] args) {
        Scanner s=new Scanner(new BufferedInputStream(System.in));
        int m=s.nextInt();
        int n=s.nextInt();
        int[][] matrix=new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                matrix[i][j]=s.nextInt();
            }
        }
        int ans=Integer.MIN_VALUE;
        for (int i = 0; i <m ; i++) {
            int[] dp=new int[n];
            for (int j = i; j < m; j++) {
                for (int k = 0; k < n; k++) {
                    dp[k]+=matrix[j][k];
                }
                int[] sum=new int[n];
                int min=0;
                for (int k = 0; k < n; k++) {
                    sum[k]+=dp[k];
                    if (k>0)sum[k]+=sum[k-1];
                    ans=Math.max(ans,sum[k]-min);
                    min=Math.min(min,sum[k]);
                }
            }

        }
        System.out.println(ans);
    }
}
```

**解法2**

动态规划

https://blog.csdn.net/seagal890/article/details/79478652?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-79478652-blog-123033169.pc_relevant_default&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-79478652-blog-123033169.pc_relevant_default&utm_relevant_index=2

```java
package com.stanlong.leetcode;

import java.io.FileNotFoundException;
import java.util.Scanner;

public class LeetCode {

    public static void main(String[] args) throws FileNotFoundException {

        Scanner sc = new Scanner(System.in);
        //读取行
        int n = sc.nextInt();
        //读取列
        int m = sc.nextInt();
        //声明一个二维数组
        int[][] matrix = new int[n][m];
        // 计算结果
        long result = Long.MIN_VALUE;

        //初始化二维数组元素
        for (int i = 0; i < n; i++)
            for (int j = 0; j < m; j++)
                //从文件中读取数据
                matrix[i][j] = sc.nextInt();

        //算法设计
        for (int start = 0; start < n; start++) { // 开始行
            long[] ring = new long[m];
            long[] dp = new long[m];
            for (int end = start; end < n; end++) { // 结束行
                for (int j = 0; j < m; j++) // 计算start~end行的每一列元素和
                    ring[j] += matrix[end][j];
                result = Math.max(result, ring[0]);
                dp[0] = ring[0];
                for (int j = 1; j < m; j++) {
                    if (dp[j - 1] < 0)
                        dp[j] = ring[j];
                    else
                        dp[j] = dp[j - 1] + ring[j];
                    result = Math.max(result, dp[j]);
                }
            }
        }

        //输出执行结果
        System.out.println(result);

    }
}
```

