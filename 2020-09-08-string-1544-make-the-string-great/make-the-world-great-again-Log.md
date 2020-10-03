#### Question [1544. 整理字符串](https://leetcode-cn.com/problems/make-the-string-great/)/[Make The String Great](https://leetcode-cn.com/problems/make-the-string-great/)

tag#string#



#### Description

```
给你一个由大小写英文字母组成的字符串 s 。

一个整理好的字符串中，两个相邻字符 s[i] 和 s[i + 1] 不会同时满足下述条件：

0 <= i <= s.length - 2
s[i] 是小写字符，但 s[i + 1] 是相同的大写字符；反之亦然 。
请你将字符串整理好，每次你都可以从字符串中选出满足上述条件的 两个相邻 字符并删除，直到字符串整理好为止。

请返回整理好的 字符串 。题目保证在给出的约束条件下，测试样例对应的答案是唯一的。

注意：空字符串也属于整理好的字符串，尽管其中没有任何字符。

 

示例 1：

输入：s = "leEeetcode"
输出："leetcode"
解释：无论你第一次选的是 i = 1 还是 i = 2，都会使 "leEeetcode" 缩减为 "leetcode" 。
示例 2：

输入：s = "abBAcC"
输出：""
解释：存在多种不同情况，但所有的情况都会导致相同的结果。例如：
"abBAcC" --> "aAcC" --> "cC" --> ""
"abBAcC" --> "abBA" --> "aA" --> ""
示例 3：

输入：s = "s"
输出："s"
 

提示：

1 <= s.length <= 100
s 只包含小写和大写英文字母
```



#### Analysis

题意分析: 一开始不是很能看懂题. 看完了解题代码后回来.

> 一个整理好的字符串中，**两个相邻字符** `s[i]` 和 `s[i + 1]` **不会同时满足下述条件**：
>
> - `0 <= i <= s.length - 2`
> - `s[i]` 是小写字符，但 `s[i + 1]` 是相同的大写字符；**反之亦然** 。

也就是说相邻的两个字符, 不可能前一个是小写字母, 后一个是同字母大写. 也不可能是前一个字母大写, 后一个同字母小写. 如果有的话, 就删除其中的大写字母.

> 请你将字符串整理好，每次你都可以从字符串中选出满足上述条件的 **两个相邻** 字符并删除，直到字符串整理好为止。

如果出现了前一位是同字母小写后一位同字母大写, 就要删除掉它们.

如 `s = "leEeetcode"`

选择相邻的 `eE` 就要删除掉后面的 `E`, 选择相邻的 `Ee` , 删除掉 `eE` 或者 `Ee` 剩下的就是 `leetcode` .

如 `s = "abBAcC"`

(目前)出现了 `bB` `cC`, 此时就要删除掉 `bB` 或者 `cC`. 删除后, 剩下原先在第一位的 `a` 和原先在第四位的 `A`  就合并到了一起, 组成了不符合要求的组合. 此时将两个删除, 最后剩下的就是 "" , 一个字符也没剩下.

解题分析:

关键是确定相邻两个字符的 acsii 码值之间的差值不能是刚好两个同字母的相对大小写.

![](https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-9-8-string-1544-make-the-string-great/ascii.jpg)

由 acsii 码值的表可得, 如果两个字符的差值为 `22` 时, 这个就可以当作是判断是否需要删除**这一对**的判断条件. 也就是属于需要删除的情况.

此时利用 `StringBuilder` 删除特定区间之间的字符, 创建实例, 并完成删除操作. 由于 `delete(start, end)` 这一操作的区间是左闭右开, 也就是 `[ start, end)` , 所以用的时候应该是设置参数为 `i, i+2`. 如代码所示.



#### Code

评论区优秀答案:

```java
class Solution {
    public String makeGood(String s) {
        StringBuilder sb = new StringBuilder(s);
        int len = -1;
        while(len != sb.length()) {
            len = sb.length();
            for (int i = 0; i < sb.length() - 1; i++) {
                if (Math.abs(sb.charAt(i) - sb.charAt(i+1)) == 'a' - 'A') { //  97-65= 32
                    sb.delete(i, i+2);
                    break;
                }
            }
        }
        return sb.toString();
    }
}
```









