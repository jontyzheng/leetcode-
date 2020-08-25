Question [最后一个单词的长度](https://leetcode-cn.com/problems/length-of-last-word/)/[Length of Last Word](https://leetcode-cn.com/problems/length-of-last-word/)

tag#String#



#### Description			

```
给定一个仅包含大小写字母和空格 ' ' 的字符串 s，返回其最后一个单词的长度。如果字符串从左向右滚动显示，那么最后一个单词就是最后出现的单词。

如果不存在最后一个单词，请返回 0 。

说明：一个单词是指仅由字母组成、不包含任何空格字符的 最大子字符串。

 

示例:

输入: "Hello World"
输出: 5
```



#### Analysis

题意分析: 已知给定的字符串只会出现 2 种类型的字符: 字母和空格.

单词的定义是: 一个不含空格的连续的字符串.

由此可知: 

```
{"   sdsd  ds "}
```

这种情况就是要找出其中 `ds` 的长度.

解题分析:

一开始的思路是两个指针分别从两头开始遍历, `j` 从后往前, 直到遇到非空格的时候, 停住, `i` 从前往后走.. 后面遇到既有空格又有字母的时候就很难确定怎么停止了.

直到翻了翻答案, 看到许多人都在抱怨题目的汉语水平.

> "a "这不是没有最后一个单词吗，是我理解错了吗
>
> 151+
>
> 我工作效率低的原因完全是因为有和力扣的题干一样语文为负分的产品经理
>
> 81+

于是打开英文版本, 马上就搜索到了关键词 `substring`, 而且还是黑体的. 这下目标就明确了. 返回中文版中标黑的却是 **最大子字符串**.

如果是找子串的话一下就清晰多了. 用空格分开后, 在拿到字符串的字符串数组后返回最后一项的长度即可.







#### Code

##### commit 1

```java
class Solution {
    public int lengthOfLastWord(String s) {
        String[] strArr = s.split(" ");        
        if (strArr.length == 0)
            return 0;        
        return strArr[strArr.length - 1].length();
    }
}
```

效果:

```
执行结果：
通过
显示详情
执行用时：
1 ms
, 在所有 Java 提交中击败了
41.21%
的用户
内存消耗：
37.9 MB
, 在所有 Java 提交中击败了
40.31%
的用户
```



事后分析:

确定思路后还因为误以为是找最大长度子串, 才有了下面的答案, 尴尬.



找出最长的字符串的长度

用空格分开, 再在字符串数组中用选择法找出其中长度最长的字符串, maxLen;

```java
class Solution {
    public int lengthOfLastWord(String s) {
        String[] strArr = s.split(" ");
        int maxLen = 0;
        if (strArr.length == 0)
            return 0;
        for (int i = 0; i < strArr.length; i++) {
            if (strArr[i].length() > maxLen) {
                maxLen = strArr[i].length();
            }
        }
        return maxLen;
    }
}
```

效果

```
执行结果：
解答错误
显示详情
输入：
"Today is a nice day"
输出：
5
预期结果：
3
```

