#### Question [剑指 Offer 40. 最小的k个数](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)

tag#剑指 offer# #排序# #数组#



#### Description

```
输入整数数组 arr ，找出其中最小的 k 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

 

示例 1：

输入：arr = [3,2,1], k = 2
输出：[1,2] 或者 [2,1]
示例 2：

输入：arr = [0,1,2,1], k = 1
输出：[0]
 

限制：

0 <= k <= arr.length <= 10000
0 <= arr[i] <= 10000

```



#### Analysis

将数组排好序后将前面 k 个数据加进结果数组即可.



#### Code

```java
class Solution {
    public int[] getLeastNumbers(int[] arr, int k) {
        // 执行用时：7 ms, 在所有 Java 提交中击败了69.27%的用户
        // 内存消耗：39.8 MB, 在所有 Java 提交中击败了91.64%的用户
        int[] target = new int[k];
        Arrays.sort(arr);
        for (int i=0; i<k; i++) {
            target[i] = arr[i];
        }
        return target;
    }
}
```







