#### Question 在区间范围内统计奇数的个数/[1523. Count Odd Numbers in an Interval Range](https://leetcode-cn.com/problems/count-odd-numbers-in-an-interval-range/)

tag#math#



#### Description

```
给你两个非负整数 low 和 high 。请你返回 low 和 high 之间（包括二者）奇数的数目。

 

示例 1：

输入：low = 3, high = 7
输出：3
解释：3 到 7 之间奇数数字为 [3,5,7] 。
示例 2：

输入：low = 8, high = 10
输出：1
解释：8 到 10 之间奇数数字为 [9] 。
 

提示：

0 <= low <= high <= 10^9

```





#### Analysis

题意分析: 找给定数字之间的奇数个数, 包括端点.

解题分析: tag 为 math, 就肯定找规律的题型. 分析如下图.



#### Code

```java
class Solution {
    public int countOdds(int low, int high) {
        // 已知 low <= high, 且都为正整数
        //  偶偶
        if (low%2 == 0 && high%2 == 0) {
            return (high - low)/2;
        } else if(low%2 == 0 && high%2 != 0){ //  偶奇            
            return (high - low)/2 + 1;            
        } else if (low%2 != 0 && high%2 != 0){
            //  奇奇
            return high/2 - low/2 + 1;
        } else {
            //  奇偶
            return (high - low)/2 + 1;
        }
    }
}
```

最主要是找 low 和 high 之间的函数表达式, 其中奇奇情况下的函数关系不那么容易找.





