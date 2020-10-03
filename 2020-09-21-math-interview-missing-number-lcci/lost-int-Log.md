#### Question 消失的数字/[面试题 17.04. 消失的数字](https://leetcode-cn.com/problems/missing-number-lcci/)

tag#math#



#### Description

```
数组nums包含从0到n的所有整数，但其中缺了一个。请编写代码找出那个缺失的整数。你有办法在O(n)时间内完成吗？

注意：本题相对书上原题稍作改动

示例 1：

输入：[3,0,1]
输出：2
 

示例 2：

输入：[9,6,4,2,3,5,7,0,1]
输出：8

```





#### Analysis

排序后找出丢失的那个, 和循环因子匹配.

如果当前部分完整的话, 这时候最后一项+1被视为丢失的一项.



#### Code

##### 常规解法

```java
class Solution {
    public int missingNumber(int[] nums) {
        Arrays.sort(nums);
        int lost = 0;
        int len = nums.length;     
        boolean hasMissed = false;   //  设置一个布尔值, 假设当前部分完整
        for (int i = 0; i < len; i++) {
            if (nums[i] != i) {
                lost = i;
                hasMissed = true;  //  发现数据有丢失, 修改布尔变量
                break;
            }
        }
        return hasMissed? lost:nums[len-1]+1;
    }
}
```

执行效果:

执行用时：6 ms, 在所有 Java 提交中击败了15.18%的用户.









