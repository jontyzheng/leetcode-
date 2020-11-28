#### Question [680. 验证回文字符串 Ⅱ](https://leetcode-cn.com/problems/valid-palindrome-ii/)

tag##



#### Description

```
给定一个非空字符串 s，最多删除一个字符。判断是否能成为回文字符串。

示例 1:

输入: "aba"
输出: True
示例 2:

输入: "abca"
输出: True
解释: 你可以删除c字符。
注意:

字符串只包含从 a-z 的小写字母。字符串的最大长度是50000。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/valid-palindrome-ii
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```





#### Analysis

给定一个字符串, 判断它是否本身就是一个回文字符串, 或者可以通过删除一个变成回文字符串.

###### 1.一个回文字符串的特点

无论奇数偶数, 从两头起字符一定两两匹配相等.

###### 2.最多删除一个后回文

是否可以通过删除一个, 有多余的一个字符的时候, 既然多余的字符出现的位置破坏了原来的对称性. 那么它的位置是已知的.

如果, 遇到这么两端不对称的位置, 那么多余的那个字符肯定就出现在这中间.

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-11-28-%E5%AD%97%E7%AC%A6%E4%B8%B2-680-%E9%AA%8C%E8%AF%81%E5%9B%9E%E6%96%87%E5%AD%97%E7%AC%A6%E4%B8%B2-%E2%85%A1/palidrome.PNG" width="60%">

但中间可能是 `ddz` 又有可能是 `zzd` 两种都可以满足要求. **两种都是对的**!

那么再判断隔一个位置两个情况如果有一种满足条件就说明中间的部分满足条件

因为只有两种情况:

要么是当前起点的后一位是多出的, 剩余的中间部分对称, 要么是当前起点到当前终点的前一位之间对称, 当前终点的前一位是多余的.

只要这两种情况有一种情况满足, 就符合结果.(所以需要 2 个布尔值变量)

###### 3.怎么判断给定区间的字符串是否对称

用两个指针判断一个字符串是否为回文字符串.

> 假设字符串为回文字符串, 那么字符串一定关于中间对称. 字符两两匹配相等.

```java
class Solution {
    public boolean isPalindrome(String s) {
        char[] chars = s.toCharArray();        
        boolean isPalindrome = true;
        int len = chars.length;
        for (int i = 0, j = len - 1; i < j; i++, j--) {            
            char x = chars[i];
            char y = chars[j];
            if (x != y) {
                isalindrome = false;
                break;
            }            
        }
        return isPalindrome;
    }
}
```





#### Code

```java
class Solution {
    //执行用时：7 ms
    public boolean validPalindrome(String s) {
        int low = 0;
        int high = s.length()-1;
        while (low < high) {
            char x = s.charAt(low);
            char y = s.charAt(high);
            if (x == y) {
                low++;
                high--;
            }
            else {
                boolean flag1 = true;
                boolean flag2 = true;
                for (int i = low, j = high - 1; i < j; i++, j--) {
                    char x1 = s.charAt(i);
                    char y1 = s.charAt(j);
                    if (x1 != y1) {
                        flag1 = false;
                        break;
                    }
                }
                for (int i = low+1, j = high; i<j; i++, j--) {
                    char x2 = s.charAt(i);
                    char y2 = s.charAt(j);
                    if (x2 != y2) {
                        flag2 = false;
                        break;
                    }
                }
                return flag1 || flag2;
            }            
        }
        return true;
    }
}
```









#### 本期心情						

学会了双指针判断对称字符串, 比栈还要简单直接.

并且原来如果一个原本对称的字符串如果多出一个的时候, 那么它只会破坏中间部分的对称.



