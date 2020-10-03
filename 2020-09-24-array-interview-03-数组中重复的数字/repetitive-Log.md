#### Question [数组中重复的数字](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

tag#剑指offer# #array#



#### Description

```
剑指 Offer 03. 数组中重复的数字
找出数组中重复的数字。


在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

示例 1：

输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
 

限制：

2 <= n <= 100000
```



#### Analysis

给定一个自然数数组 ( 0 +正整数), 找出其中任意一个重复的数字.

只要找到其中一个符合条件的就可以了.

所以排序后, 连续出现两次的就是一个满足条件的结果了.



#### Code

```java
class Solution {
    public int findRepeatNumber(int[] nums) {
       Arrays.sort(nums);
       int len = nums.length;
       int x = -1;
       for (int i=0; i < len; i++) {
           if (nums[i+1] == nums[i]) {
               x = nums[i];
               break;
           }
       }
       return x;
    }
}
```



运行效果:

执行结果：

通过

显示详情

执行用时：3 ms, 在所有 Java 提交中击败了60.14%的用户





