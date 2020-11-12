#### Question [1624. 两个相同字符之间的最长子字符串](https://leetcode-cn.com/problems/largest-substring-between-two-equal-characters/)

tag##



#### Description

```
给你一个字符串 s，请你返回 两个相同字符之间的最长子字符串的长度 ，计算长度时不含这两个字符。如果不存在这样的子字符串，返回 -1 。

子字符串 是字符串中的一个连续字符序列。

 

示例 1：

输入：s = "aa"
输出：0
解释：最优的子字符串是两个 'a' 之间的空子字符串。
示例 2：

输入：s = "abca"
输出：2
解释：最优的子字符串是 "bc" 。
示例 3：

输入：s = "cbzxy"
输出：-1
解释：s 中不存在出现出现两次的字符，所以返回 -1 。
示例 4：

输入：s = "cabbac"
输出：4
解释：最优的子字符串是 "abba" ，其他的非最优解包括 "bb" 和 "" 。
 

提示：

1 <= s.length <= 300
s 只含小写英文字母

```





#### Analysis

###### 【精华浓缩版】

另一头相同字符出现的位置(从前往后最后出现的位置) = 从后往前第一个出现的位置.



###### 【详解版】

题目意思是, 给定一个字符串, 找出两个相同字符中最多隔了多少个字符.

1.找字符串两头相同字符的坐标.

首先想到的思路就是双指针遍历, 前后匹配. 当两头的字符匹配时, 计算中间的字符个数. `j-i-1`. 但是遇到一个测试用例就发现了这种做法出错的地方:

假如两个字符不是位于对称的位置呢? 那它们很明显就不是同步的.

2.不同步、找两端相同的字符出现的出现.

然后就想到了 `indexOf` 可是 `indexOf` 只能找字符**首次**出现的位置.

首次出现的位置(找一头的) 实际情况的字符又可能出现多次, 那最多, 正方向首次出现, 和反方向第一次出现中间相隔的不就是它们最长的子串吗?

于是, 可以反向排序字符串, 然后使用 `indexOf` 找出当前字符在那边的坐标

3.找到两头相同的字符的位置后(后一个位置是相对于最后一个的位置), 顺序的转换.

需要将反方向排第几, 转换成正方向排第几才可以.

当然, 要确保转换后的序号要在当前坐标的**右边**, 才可以通过 `j-i-1` 计算中间的长度.

4.最大长度就用一个 `Math.max()` 取最大值.



注意:

反向第 `i` 个 = 正向第 `len - i - 1` 个

两个坐标中间的长度("开区间")为 `j - i - 1`



通过手动测试一个测试用例发现方案可行.



#### Code

```java
class Solution {
    //执行用时：1 ms, 在所有 Java 提交中击败了81.73%的用户
    public int maxLengthBetweenEqualCharacters(String s) {        
        //  逆序字符串 rev, 用于找字符在反方向首次出现的位置
        StringBuilder sbu = new StringBuilder(s);
        String rev = sbu.reverse().toString();

        int len = s.length();

        int maxNums = -1;
        for (int i = 0; i < len-1; i++) {        
            char c = s.charAt(i);            
            int revIndex = rev.indexOf(c);

            if (revIndex >= 0) {                
                int relativePos = len - revIndex - 1;
                if (relativePos > i) {                
                    int count = relativePos - i - 1;                                          
                    maxNums = Math.max(maxNums, count);                
                }                
            }             
        }
        return maxNums;
    }
}
```





​			





