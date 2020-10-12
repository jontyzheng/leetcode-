#### Question [剑指 Offer 39. 数组中出现次数超过一半的数字](https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/)

tag#剑指 offer# #数组#



#### Description

```
数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。

 

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

 

示例 1:

输入: [1, 2, 3, 2, 2, 2, 5, 4, 2]
输出: 2
 

限制：

1 <= 数组长度 <= 50000

```

注意：本题与主站 169 题相同：https://leetcode-cn.com/problems/majority-element/



#### Analysis

如注释所示.



#### Code

##### commit 

```java
class Solution {
    public int majorityElement(int[] nums) {
        // 执行用时：1787 ms, 在所有 Java 提交中击败了5.11%的用户
        // 内存消耗：41.7 MB, 在所有 Java 提交中击败了97.51%的用户
        int len = nums.length;
        int targetTimes = len/2;
        int target = -1;        
        Arrays.sort(nums);
        for (int i=0; i<len; i++) {
            int count = getFrequency(nums, nums[i]);
            if (count > targetTimes) {
                target = nums[i];
                break;
            }
        }
        return target;
    }
    //  在一个排好序的数组中找指定元素的个数
    public int getFrequency (int[] nums, int x) {
        int count = 0;
        int i=0;
        while (i<nums.length) {
            if (nums[i] == x) {
                count++;
            }
            i++;
        }
        return count;
    }
}
```

##### commit

受到第一次的启发, 如果一个数组中总存在多数元素, 且那个元素总超过数组长度的一半的话:

那么经过排序, 相同的并列在一起, 那么, 它从首次出现的位置, 依次到后面 len-1 的位置, 肯定还是它. 即拿只要当前元素和第 当前下标+len/2 地方的位置一对比, 就可以知道有没有遍历到目标项了.

```java
class Solution {
    public int majorityElement(int[] nums) {
        // 执行用时：3 ms, 在所有 Java 提交中击败了34.78%的用户
        // 内存消耗：41.8 MB, 在所有 Java 提交中击败了88.60%的用户
        int len = nums.length;
        int targetTimes = len/2;
        int target = -1;
        Arrays.sort(nums);
        for (int i=0; i<len; i++) {            
            if (nums[i] == nums[i+len/2]) {     
                target = nums[i];        
                break;        
            }
        }
        return target;
    }
}
```





