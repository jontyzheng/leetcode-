#### Question 旋转数字的最小数字

tag#剑指 offer# #array#



#### Description

```
把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一个旋转，该数组的最小值为1。  

示例 1：

输入：[3,4,5,1,2]
输出：1
示例 2：

输入：[2,2,2,0,1]
输出：0
```

注意：本题与主站 154 题相同：[154. 寻找旋转排序数组中的最小值 II](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/)



#### Analysis

最后返回数组中最小的数字.



#### Code

```java
class Solution {
    public int minArray(int[] numbers) {
        // 执行用时：1 ms, 在所有 Java 提交中击败了45.02%的用户
		// 内存消耗：38.6 MB, 在所有 Java 提交中击败了51.50%的用户
        Arrays.sort(numbers);
        return numbers[0];
    }
}
```





