#### Question [剑指 Offer 21. 调整数组顺序使奇数位于偶数前面](https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/)

tag#剑指 offer# #array# #奇数和偶数#



#### Description

```
输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有偶数位于数组的后半部分。

 

示例：

输入：nums = [1,2,3,4]
输出：[1,3,2,4] 
注：[3,1,2,4] 也是正确的答案之一。
 

提示：

1 <= nums.length <= 50000
1 <= nums[i] <= 10000

```



#### Analysis





#### Code

```java
class Solution {
    public int[] exchange(int[] nums) {
        // 执行用时：3 ms, 在所有 Java 提交中击败了34.19%的用户    
        // 内存消耗：46.8 MB, 在所有 Java 提交中击败了38.49%的用户
        int temp = 0;
        int i=0;
        int j=0;
        while(i<nums.length) {
            if (nums[i] % 2 == 1) {
                temp = nums[j]; 
                nums[j] = nums[i];
                nums[i] = temp;
                j++;
            }
            i++;
        }
        return nums;
    }
}
```





