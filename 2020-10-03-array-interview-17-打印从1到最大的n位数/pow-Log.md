#### Question [剑指 Offer 17. 打印从1到最大的n位数](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)

tag#剑指 offer# #math# #array#



#### Description

```
输入数字 n，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。

示例 1:

输入: n = 1
输出: [1,2,3,4,5,6,7,8,9]
 

说明：

用返回一个整数列表来代替打印
n 为正整数

```

举例:

```
输入: n = 1
输出: [1,2,3,4,5,6,7,8,9]
输入：n = 2
预期结果: [1~99]
```

当 n = 1 时, 数组有 9 项, 当 n = 2 时从数组从 1 ~ 99, 长度为 99.

#### Analysis

输入的 n 表示 0 的个数, 要求输出 1~(n-1) 之间的连续整数.

长度应该用 `Math.pow(n, m)` , 但是它**返回 double 类型**. 因为 Java 中的 `^ ` 是一个**逻辑运算符**.

数组内的元素值和 `i` 勾连起来.



#### Code

```java
class Solution {
    public int[] printNumbers(int n) {
        // 执行用时：1 ms, 在所有 Java 提交中击败了99.98%的用户
        // 内存消耗：46.9 MB, 在所有 Java 提交中击败了33.77%的用户
        //  pow() 返回 double 类型的结果
        int len = (int)Math.pow(10, n)-1;              
        int[] arr = new int[len];        
        for (int i=0; i<len; i++) {
            arr[i] = i+1;
        }
        return arr;
    }
}
```







