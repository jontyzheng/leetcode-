#### Question [1408. 数组中的字符串匹配](https://leetcode-cn.com/problems/string-matching-in-an-array/)

tag##



#### Description

```
给你一个字符串数组 words ，数组中的每个字符串都可以看作是一个单词。请你按 任意 顺序返回 words 中是其他单词的子字符串的所有单词。

如果你可以删除 words[j] 最左侧和/或最右侧的若干字符得到 word[i] ，那么字符串 words[i] 就是 words[j] 的一个子字符串。

 

示例 1：

输入：words = ["mass","as","hero","superhero"]
输出：["as","hero"]
解释："as" 是 "mass" 的子字符串，"hero" 是 "superhero" 的子字符串。
["hero","as"] 也是有效的答案。
示例 2：

输入：words = ["leetcode","et","code"]
输出：["et","code"]
解释："et" 和 "code" 都是 "leetcode" 的子字符串。
示例 3：

输入：words = ["blue","green","bu"]
输出：[]
 

提示：

1 <= words.length <= 100
1 <= words[i].length <= 30
words[i] 仅包含小写英文字母。
题目数据 保证 每个 words[i] 都是独一无二的。


```



#### Analysis

问题要求: 给定一组字符串, 已知其中有几个字符串是其它字符串的一个子串, 字符串数组可以保证字符串不重复, 现要找出这些可以组成其它字符串的**项**.

1.字符串相互比较有 API `contains(String str)`;

2.长的字符串不可能是短的字符串的子串;

3.常规思路即可, "字符串之间相互比较"的思路太南了, 只要从头到尾遍历过去, 长度满足条件后再判断是否后面有一个字符串 contains 当前字符串就可以收入囊中.

4.最重要的一点: 只要确认当前项是组成其它字符串的子串就行了. 匹配成功就可以结束本轮怼当前项的判断了.



#### Code

```java
class Solution {
    //执行用时：7 ms    
    public List<String> stringMatching(String[] words) {
        int len = words.length;
        if (len == 1)
            return null;
        List<String> matched = new ArrayList<>();   /*返回值提示*/
        for (String word : words) {
            for (int i = 0; i < len; i++) {
                if (!word.equals(words[i])) {
                    if (word.length() >= words[i].length())
                        continue;                
                    else if (words[i].contains(word)) {
                        matched.add(word);    
                        break;                
                    } 
                }                               
            }
        }
        return matched;
    }
}
```



##### 	【本题小结】

常规思路可解





