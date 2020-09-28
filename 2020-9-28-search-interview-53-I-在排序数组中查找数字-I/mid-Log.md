#### Question [剑指 Offer 53 - I. 在排序数组中查找数字 I](https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/)

tag#剑指 offer# #sort#  #array# 



#### Description

```
统计一个数字在排序数组中出现的次数。

 

示例 1:

输入: nums = [5,7,7,8,8,10], target = 8
输出: 2
示例 2:

输入: nums = [5,7,7,8,8,10], target = 6
输出: 0
 

限制：

0 <= 数组长度 <= 50000
```



#### Analysis

已知数组排序, 在 50000 个数组中找一个数, 并得出该数字出现的次数. 首先想到二分法.



#### Code

```java
class Solution {
    public int search(int[] nums, int target) {
        // 执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
        // 内存消耗：41.5 MB, 在所有 Java 提交中击败了87.73%的用户
        int len = nums.length;
        // 不能用二分法, 如果刚好分布在中点两端的话, 影响计数
        int left = 0;
        int right = len-1;
        int count = 0;
        while (left < right) {
            int mid = (left+right)/2;
            if (nums[mid] >= target)
                right = mid;
            if (nums[mid]<target)
                left = mid+1;
        }
        while (left<len && nums[left++] == target)
            count++;
        return count;
    }
}
```







