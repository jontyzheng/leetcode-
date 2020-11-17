#### Question [上升下降字符串](https://leetcode-cn.com/problems/increasing-decreasing-string/)/[Increasing Decreasing String](https://leetcode-cn.com/problems/increasing-decreasing-string/)

tag#String#



#### Description

```
给你一个字符串 s ，请你根据下面的算法重新构造字符串：

从 s 中选出 最小 的字符，将它 接在 结果字符串的后面。
从 s 剩余字符中选出 最小 的字符，且该字符比上一个添加的字符大，将它 接在 结果字符串后面。
重复步骤 2 ，直到你没法从 s 中选择字符。
从 s 中选出 最大 的字符，将它 接在 结果字符串的后面。
从 s 剩余字符中选出 最大 的字符，且该字符比上一个添加的字符小，将它 接在 结果字符串后面。
重复步骤 5 ，直到你没法从 s 中选择字符。
重复步骤 1 到 6 ，直到 s 中所有字符都已经被选过。
在任何一步中，如果最小或者最大字符不止一个 ，你可以选择其中任意一个，并将其添加到结果字符串。

请你返回将 s 中字符重新排序后的 结果字符串 。

 

示例 1：

输入：s = "aaaabbbbcccc"
输出："abccbaabccba"
解释：第一轮的步骤 1，2，3 后，结果字符串为 result = "abc"
第一轮的步骤 4，5，6 后，结果字符串为 result = "abccba"
第一轮结束，现在 s = "aabbcc" ，我们再次回到步骤 1
第二轮的步骤 1，2，3 后，结果字符串为 result = "abccbaabc"
第二轮的步骤 4，5，6 后，结果字符串为 result = "abccbaabccba"
示例 2：

输入：s = "rat"
输出："art"
解释：单词 "rat" 在上述算法重排序以后变成 "art"
示例 3：

输入：s = "leetcode"
输出："cdelotee"
示例 4：

输入：s = "ggggggg"
输出："ggggggg"
示例 5：

输入：s = "spo"
输出："ops"
 

提示：

1 <= s.length <= 500
s 只包含小写英文字母。
```



#### Analysis

题意分析: 将原字符串构造成一个呈水平线或者锯齿状的序列.

如 `aaaabbbbcccc` 按题目要求排序后的顺序就是 `abccbaabc`, 如果按照折线图的形式就是 `↗↘↗`

`rat` 排序后的序列就是 `art` 图像就是 `↗`

`ggggg` 只含有一个字母的字符串就还是原序列, 呈水平线. 图像为 `→`



解题分析: 暂时还没想到很好的方法 答案参考评论区.



#### Code

评论区优秀答案 | 3ms

```java
class Solution {
    public String sortString(String s) {
        StringBuilder builder = new StringBuilder();
        int[] map = new int[26];
        for (char c : s.toCharArray())
            map[c - 'a']++; //  第 i-a 位++
        boolean flag;
        do {
            flag = false;
            for (int i = 0; i < 26; i++) {
                if (map[i] > 0) {
                    builder.append((char) (i + 'a'));
                    map[i]--;
                    flag = true;
                }
            }
            for (int i = 25; i >= 0; i--) {
                if (map[i] > 0) {
                    builder.append((char) (i + 'a'));
                    map[i]--;
                    flag = true;
                }
            }
        } while (flag);
        return builder.toString();

    }            
}

```



优秀答案2 | 4ms

```java
public static String sortString2(String s) {
		StringBuilder sb = new StringBuilder();
		int[] alphabet = new int[28];
		for (char c : s.toCharArray())
			alphabet[c - 'a' + 1]++;
		int i = 0, n = 1;
		boolean b = true;
		while (i < s.length()) {
			if (alphabet[n] > 0) {
				sb.append((char) (n + 'a' - 1));
				alphabet[n]--;
				i++;
			}
			if (n == 27)
				b = false;
			if (n == 0)
				b = true;
			n += b ? 1 : -1;
		}
		return sb.toString();
	}
```







