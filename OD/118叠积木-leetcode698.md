# 叠积木

积木宽高相等，长度不等，每层只能放一个或拼接多个积木，每层长度相等，求最大层数，最少2层。 

**输入**：

- 给定积木的长度，以空格分隔，例如:3 6 6 3。 

**输出**：

- 如果可以搭建，返回最大层数，如果不可以返回-1。 

**例1：**

```
输入：3 6 6 3

输出：3 

说明：3 6 6 3 有两种组合
第一种两层：第一层6+3， 第二层6+3
第二种三层：第一层6，第二层6，第三层3+3。
题目要求返回最大层数，因此返回3
```

**例2：**  

```
输入：3 5  
输出：-1
```

```java
import java.util.*;
publicclass Main {
publicstaticvoid main(String[] args) {
        Scanner in = new Scanner(System.in);
        String inStr = in.nextLine();
        String[] inStrs = inStr.split(" ");
int inLen = inStrs.length;
int[] brickLength = newint[inLen];      //积⽊长度
        Map<Integer, Integer> lenMap = new HashMap();
for (int i = 0; i < inLen; i++) {
int length = Integer.parseInt(inStrs[i]);
            brickLength[i] = length;
int count = 1;
if (lenMap.containsKey(length)) count += lenMap.get(length);        //如果原来有此数，则加上1
            lenMap.put(length, count);
        }
        Map<Integer, int[]> brick2LengthMap = new HashMap(); int index = 0;
for (int i = 0; i < inLen; i++) {
for (int j = 1; j < inLen; j++) {
                brick2LengthMap.put(index++, newint[]{i, j, brickLength[i] + brickLength[j]});
            }
        }
        Set<Integer> set = new HashSet();
        Set<Integer> seti = new HashSet();
int eq2Count;        //相同长度积⽊的⾄少个数
for (int i = inLen; i > (inLen - 1) / 2; i--) {
            eq2Count = inLen - i;       //如果此为⼀层，则两块积⽊。2-4,3-6
int[] eqs = newint[eq2Count];
long counteqs = 0;
for (int j = 1; j <= eqs.length; j++) {
                counteqs += Math.pow(brick2LengthMap.size(), j);
            }
for (int j = 0; j < counteqs; j++) {
int temp = j;seti.clear();set.clear();
for (int k = eqs.length - 1; k >= 0 ; k--) {
int i1 = (int) (temp / Math.pow(brick2LengthMap.size(), k));
int[] ints = brick2LengthMap.get(i1);
                    temp = temp - (int) (i1 * Math.pow(brick2LengthMap.size(), k));
if (seti.contains(ints[0]) || seti.contains(ints[1])) break;
                    seti.add(ints[0]);seti.add(ints[1]);
                    set.add(ints[2]);
                }
if (set.size() > 1) continue;       //针对上⾯的进⾏跳出
for (int k = 0; k < brickLength.length; k++) {
if (seti.contains(k)) continue;
                    set.add(brickLength[k]);
if (set.size() > 1) break;
                }
if (set.size() == 1) {
                    System.out.println(i);
return;
                }
            }
        }
        System.out.println(-1); return;
    }
}
```



   