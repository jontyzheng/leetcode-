#### Question [面试题 01.04. 回文排列](https://leetcode-cn.com/problems/palindrome-permutation-lcci/)

tag#字符串# #回文# #巧用集合类#



#### Description

```
给定一个字符串，编写一个函数判定其是否为某个回文串的排列之一。

回文串是指正反两个方向都一样的单词或短语。排列是指字母的重新排列。

回文串不一定是字典当中的单词。

 

示例1：

输入："tactcoa"
输出：true（排列有"tacocat"、"atcocta"，等等）

```



#### Analysis

可以构成回文字符串的有 2 种:

一种是偶数个字符, 每个(种)字符必须成对存在: 如 aabb - abba;

一种是奇数个字符, 出现次数为奇数的字符有且仅有一次: 如 aab - aba, aabbb - abbba.

这里用的方法把 Set 当一个容器来用. 通过遇双移除, 遇单添加的机制筛选出达到条件的字符串.

和"用栈处理平衡符号"的思路很像.

最后留下的有且仅有 0 个或 1 个字符. 刚好对应上面的 2 种情况.



#### Code

```java
class Solution {
    // 执行用时：1 ms, 在所有 Java 提交中击败了71.57% 的用户
    // 内存消耗：35.9 MB, 在所有 Java 提交中击败了98.83% 的用户
    public boolean canPermutePalindrome(String s) {
        if (s == null)
            return false; 
        char[] arr = s.toCharArray();     
        Set<Character> set = new HashSet<>();
        for (char c : arr) {
            if (set.contains(c)) {
                set.remove(c);
            } else {
                set.add(c);
            }
        }
        return set.size() <= 1;
    }
}
```







