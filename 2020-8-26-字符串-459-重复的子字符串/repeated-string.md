#### Question [重复的子字符串](https://leetcode-cn.com/problems/repeated-substring-pattern/)/[Repeated Substring Pattern](https://leetcode-cn.com/problems/repeated-substring-pattern/)

tag#String#



#### Description

```
给定一个非空的字符串，判断它是否可以由它的一个子串重复多次构成。给定的字符串只含有小写英文字母，并且长度不超过10000。

示例 1:

输入: "abab"

输出: True

解释: 可由子字符串 "ab" 重复两次构成。
示例 2:

输入: "aba"

输出: False
示例 3:

输入: "abcabcabcabc"

输出: True

解释: 可由子字符串 "abc" 重复四次构成。 (或者子字符串 "abcabc" 重复两次构成。)

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/repeated-substring-pattern
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```



#### Analysis

题目分析: 给定一个字符串, 看它是不是只由某一个字串复制粘贴构成的.

解题分析:

一开始是没有什么思路的

先是看到评论区的一个回答: 依次循环整个字符串, 每次将 (0, i) 作为一个子串, 判断整个字符串是不是它的倍数.

然后是看到另一个答案. 也是最后觉得不错的方法.

假设是一个满足条件的字符串, 那么, 可以把它分成两部分. 一部分是最小子串, 另一部分是后半部分.

如 `weeweewee` 的最小字符串为 `wee`, 那么后半部分就是 `weeweewee`.

那么既然这个字符串是由一个子串组合而成的, 那么在倍数不变的情况下, 无论怎么组合都是和原来相等的. 像搭火车积木一样.

同一节车厢, 不管是放在开头, 还是最后, 还是原来的那条火车.

所以, 这里也可以类比, 符合这个 "火车" 特征的字符串肯定也是和这辆火车是一样的. 如果把第一节车厢放到最后一节拼上去, 还是和原来的火车一模一样.

所以, 利用字符串的 API: +. 就可以实现这种验证.



#### Code

##### commit 1

```java
class Solution {
    public boolean repeatedSubstringPattern(String s) {
        for (int i = 1; i <= s.length()/2; i++) {
            if (s.length() % i == 0 && s.equals(s.substring(i) + s.substring(0, i))) {
                return true;
            }
        }
        return false;
    }
}
```



这个答案还有一个优秀的地方在作者在找子串的时候认识到了在找的时候如果字符串不是 `i` 的倍数那也是白搭. 

一个这样的重复字符串的长度一定是子串长度的倍数.



#### 事后分析

利用假设法, 假设是目标是一个符合要求的对象, 那么确定它可能遵循的规律, 想办法验证目标符不符合这种规律.



