# We Are A Team

https://blog.csdn.net/weixin_39758048/article/details/111341442

总共有n个人在机房，每个人有一个标号（1 <= 标号 <=n），他们分成了多个团队，需要你根据收到的m条消息判定指定的两个人是否在一个团队中，具体的：

- 消息构成为：a b c，整数a、b分别代表了两个人的标号，整数c代表指令。
- c==0代表a和b在一个团队内。
- c==1代表需要判定a和b的关系，如果a和b是一个团队，输出一行“we are a team”，如果不是，输出一行“we are not a team”。
- c为其它值，或当前行a或b超出1~n的范围，输出`“da pian zi”`。

**输入描述:**

- 第一行包含两个整数n, m(1 <= n, m <= 100000)，分别表示有n个人和m条消息。
- 随后的m行，每行一条消息，消息格式为:a b c (1 <= a, b <= n, 0 <= c <= 1)。

**输出描述:**

- c==1时，根据a和b是否在一个团队中输出一行字符串，在一个团队中输出“we are a team”，不在一个团队中输出“we are not a team”。
- c为其他值，或当前行a或b的标号小于1或者大于n时，输出字符串`“da pian zi”`。
- 如果第一行n和m的值超出约定的范围时，输出字符串"NULL"。

**示例1**

```
输入
5 6
1 2 0
1 2 1
1 5 0
2 3 1
2 5 1
1 3 2

输出
we are a team
we are not a team
we are a team
da pian zi

说明
第2行定义了1和2是一个团队
第3行要求进行判定，输出"we are a team"
第4行定义了1和5是一个团队，自然2和5也是一个团队
第5行要求进行判定，输出"we are not a team"
第6行要求进行判定，输出"we are a team"
第7行c为其它值，输出"da pian zi"
```

```java
package com.stanlong.leetcode;

import java.io.BufferedInputStream;
import java.util.*;

/**
 * We Are A Team
 */
public class LeetCode {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(new BufferedInputStream(System.in));
        int n = scanner.nextInt();
        int m = scanner.nextInt();
        int[][] matrix = new int[m][3];
        for(int i=0; i< matrix.length; i++){
            for(int j=0; j<3; j++){
                matrix[i][j] = scanner.nextInt();
            }
        }

        Map<Integer, HashSet<Integer>> map = new HashMap<>();
        for(int i=0; i< matrix.length; i++){
            int a = matrix[i][0];
            int b = matrix[i][1];
            int c = matrix[i][2];

            switch (c){
                case 0:
                    if(!map.containsKey(a) && !map.containsKey(b)){
                        HashSet<Integer> set = new HashSet<>();
                        set.add(a);
                        set.add(b);
                        map.put(a, set);
                        map.put(b, set);
                    }else if(map.containsKey(a)){
                        HashSet<Integer> set = map.get(a);
                        set.add(b);
                        map.put(b, set);
                    }else if(map.containsKey(b)){
                        HashSet<Integer> set = map.get(b);
                        set.add(a);
                        map.put(a, set);
                    }
                    break;
                case 1:
                    if(!map.containsKey(a) && !map.containsKey(b)){
                        System.out.println("we are not a team");
                    }else if(map.containsKey(a)){
                        System.out.println(map.get(a).contains(b)?"we are a team":"we are not a team");
                    }else if(map.containsKey(b)){
                        System.out.println(map.get(b).contains(a)?"we are a team":"we are not a team");
                    }
                    break;
                default:
                    System.out.println("da pian zi");
            }

        }
    }
}
```

