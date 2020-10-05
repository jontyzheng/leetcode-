#### Question [剑指 Offer 61. 扑克牌中的顺子](https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/)

tag#剑指 offer# #sort# #array#



#### Description

```
从扑克牌中随机抽5张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王为 0 ，可以看成任意数字。A 不能视为 14。

 

示例 1:

输入: [1,2,3,4,5]
输出: True
 

示例 2:

输入: [0,0,1,2,5]
输出: True
 

限制：

数组长度为 5 

数组的数取值为 [0, 13] .
```



#### Analysis

主要是看数组相邻两项之前的差值是否可以用前面 0 的个数刚好填满.

需要注意的是

1.相邻两项之间相差 2, 只需一个 0;

2.给定数组参数不一定有序.



#### Code

```java
class Solution {
    public boolean isStraight(int[] nums) {
        // 执行用时：1 ms, 在所有 Java 提交中击败了91.16%的用户
        // 内存消耗：36.4 MB, 在所有 Java 提交中击败了65.15%的用户
        Arrays.sort(nums);
        int count = 0;
        int len  = nums.length;
        boolean isStraight = true;
        // 从第一个不是 0 的项开始计算和后一项的差值, 拿差值和前方 0 的个数相比较
        for (int i=0; i<len-1; i++) {            
            if (nums[i] == 0) {
                count++;
            }
            if (nums[i] != 0) {
                int diff = nums[i+1]-nums[i];
                if (diff == 0)  {       //  排除对子的情况
                    isStraight = false;
                    break;
                }     
                // 先看判断相邻两项的差值是否大于 1
                if (diff > 1) {                    
                    // 再看前面的 0 够不够填: diff <= count+1 
                    if (diff > (count+1)) {
                        isStraight = false;
                        break;  
                    }
                    // 够的话每次减去 (diff - 1) 个 0
                    int s = 1;
                    while (s<diff) {
                        count--;
                        s++;
                    }                                                                
                }
            }
        }
        return isStraight;
    }
}
```







