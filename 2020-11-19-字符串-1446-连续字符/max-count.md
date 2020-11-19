#### Question [1446. 连续字符](https://leetcode-cn.com/problems/consecutive-characters/)

tag##



#### Description

```
给你一个字符串 s ，字符串的「能量」定义为：只包含一种字符的最长非空子字符串的长度。

请你返回字符串的能量。

 

示例 1：

输入：s = "leetcode"
输出：2
解释：子字符串 "ee" 长度为 2 ，只包含字符 'e' 。
示例 2：

输入：s = "abbcccddddeeeeedcba"
输出：5
解释：子字符串 "eeeee" 长度为 5 ，只包含字符 'e' 。
示例 3：

输入：s = "triplepillooooow"
输出：5
示例 4：

输入：s = "hooraaaaaaaaaaay"
输出：11
示例 5：

输入：s = "tourist"
输出：1
 

提示：

1 <= s.length <= 500
s 只包含小写英文字母。


```



#### Analysis

##### 1.字符串的能量是什么?

相同字符最多连续出现的次数 (能量? 一口气能憋多少口气吗?). 

##### 2.例子

这一题的第一个例子描述得就十分清晰了:

```
输入：s = "leetcode"
输出：2
解释：子字符串 "ee" 长度为 2 ，只包含字符 'e' 。
```

记录字符串中, 由一个字符构成的最长子串的长度.

##### 3.方法

这不就和前不久做到的一道题很像, 就是另外开一个循环因子从下一个字符开始比较, 找连续出现最长的次数.

具体: 循环当前字符, 另外开一个循环因子 k. k<sub>0</sub> = i + 1, 直到最后一项. 如果相同则让当前 i 项的计数器加数, 遇到不同的就停下, 比较累计的数量, 然后和最大比较取最大.



##### 4.优化

如果计数器累加到超过 1 的时候, 下一次循环可以从那个地方开始比较, 中间的相同字符不用重复计数了.



#### Code

```java
class Solution {
    //执行用时：2 ms
    public int maxPower(String s) {
        int maxCount = 1;
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            int cnt = 1;            
            for (int k = i+1; k < s.length(); k++) {
                char next = s.charAt(k);
                if (next == c) {
                    cnt++;
                }
                else {                    
                    break;
                }                
            }    
            maxCount = cnt > maxCount? cnt : maxCount;            
        }
        return maxCount;
    }
}
```

优化:

```java
class Solution {
    //执行用时：2 ms
    public int maxPower(String s) {
        int maxCount = 1;
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            int cnt = 1;            
            for (int k = i+1; k < s.length(); k++) {
                char next = s.charAt(k);
                if (next == c) {
                    cnt++;
                }
                else {                    
                    break;
                }                
            }    
            maxCount = cnt > maxCount? cnt : maxCount;  
            i = i + cnt - 1;        
            /*优化: 下一次可以从最后一次出现的地方开始 (i+cnt)-1 减去循环体后的自增*/  
        }
        return maxCount;
    }
}
```





#### 本期心情						

虽然优化没有体现出效果, 但还是有必要改进的.



