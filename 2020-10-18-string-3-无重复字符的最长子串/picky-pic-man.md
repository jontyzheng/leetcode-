#### Question [3. 无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

tag#字符串# #middle#



#### Description

```
给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

示例 1:

输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
示例 2:

输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
示例 3:

输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。

```



#### Analysis

题目的要求嘛, 主要是找出其中不含重复字母的最长子串.

即子串需要满足的条件是: 不能含有相同的字符. 

这样题目就分成了两部分: ① 连续子串不能含有同一个字符超过 1 次. ② 再找其中最大的.

如果考虑追加的话, 遇到一个字母就要判断已有的字符串是否含有再追加, 那样势必要多一层对"已有字符串"遍历判断的 for 循环.

所以, 根据题目的要求, 我理解成一次性最多可以吃多少个字母. 是的, 有点像那个**吃豆人**.

![](https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-10-18-string-3-%E6%97%A0%E9%87%8D%E5%A4%8D%E5%AD%97%E7%AC%A6%E7%9A%84%E6%9C%80%E9%95%BF%E5%AD%90%E4%B8%B2/pac-man.png)

遇到**没见过的**才吃, 看最后吃的最长的豆子.

判含就很自然想到了 Collection 的 contains, 所以就想到了 List. 另外, 一方面用 contains 对集合内的数据进行判含, 一方面用 add 吃豆子. 

最长就采用了打擂台的形式. 





#### Code

```java
class Solution {
    // 执行用时：783 ms, 在所有 Java 提交中击败了5.01%的用户
    // 内存消耗：38.5 MB, 在所有 Java 提交中击败了98.32%的用户
    public int lengthOfLongestSubstring(String s) {
        //  一次性最多可以吃下多少个互不相同的字母        
        char[] arr = s.toCharArray();
        int len = arr.length;
        if (len == 0)
            return 0;    
        if (len == 1)    
            return 1;
        //  List 可以利用 contains 验含
        List<Character> longest = new ArrayList<>();        
        for (int i=0; i<len-1; i++) {
            List<Character> list = new ArrayList<>();
            list.add(arr[i]);
            for (int j=i+1; j<len; j++) {
                char c = arr[j];
                if (list.contains(c) == false) {
                    list.add(c);
                } else {
                    break;
                }                 
            }
            if (list.size() > longest.size())
                longest = list;            
        }
        return longest.size();
    }
}
```





对, 就是这么一个吃豆子游戏 - 无重复的最长子串.

![](https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-10-18-string-3-%E6%97%A0%E9%87%8D%E5%A4%8D%E5%AD%97%E7%AC%A6%E7%9A%84%E6%9C%80%E9%95%BF%E5%AD%90%E4%B8%B2/pac-head.gif)

