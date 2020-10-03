#### Question [242. 有效的字母异位词](https://leetcode-cn.com/problems/valid-anagram/)/[Valid Anagram](https://leetcode-cn.com/problems/valid-anagram/)

tag#sort#



#### Description

```
给定两个字符串 s 和 t ，编写一个函数来判断 t 是否是 s 的字母异位词。

示例 1:

输入: s = "anagram", t = "nagaram"
输出: true
示例 2:

输入: s = "rat", t = "car"
输出: false
说明:
你可以假设字符串只包含小写字母。
```



#### Analysis

题意分析: 异位词, 顾名思义, 两个字符串由相同的字符组成, 但是字符的排列顺序不一样.

解题分析: 将它们排好序, 判断相等不相等即可.



#### Code

效果:

执行用时：3 ms, 在所有 Java 提交中击败了86.54%的用户

内存消耗：39.7 MB, 在所有 Java 提交中击败了88.70%的用户



```java
class Solution {
    public boolean isAnagram(String s, String t) {
        char[] s1 = s.toCharArray();
        char[] s2 = t.toCharArray();
        Arrays.sort(s1);
        Arrays.sort(s2);
        return Arrays.equals(s1, s2);
    }
}
```







