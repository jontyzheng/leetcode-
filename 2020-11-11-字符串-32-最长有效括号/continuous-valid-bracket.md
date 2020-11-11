#### Question [32. 最长有效括号](https://leetcode-cn.com/problems/longest-valid-parentheses/)

tag##



#### Description

```
给定一个只包含 '(' 和 ')' 的字符串，找出最长的包含有效括号的子串的长度。

示例 1:

输入: "(()"
输出: 2
解释: 最长有效括号子串为 "()"
示例 2:

输入: ")()())"
输出: 4
解释: 最长有效括号子串为 "()()"

输入: "()(()"
输出: 2
解释: 子串要求连续
```



#### Analysis

问题: 统计字符串中有效括号的个数

首先看到题目, 我就把想出了 3 种它需要计数的基本情况:

```
((()))	==6
()()	==4
(())()	==6
```

连续邻近的括号匹配很容易让人想到栈:

> 遇 `(` 入栈
>
> 遇 `)` 与栈中最近的匹配

于是就有了

```java
class Solution {
    public int longestValidParentheses(String s) {        
        if (s.length() <= 1)
            return 0;
        Stack<Character> stack = new Stack<>();
        int count = 0;
        for (char c : s.toCharArray()) {            
            if (c == '(') {
                stack.push(c);
            }
            else if (c == ')') {                
                if (!stack.isEmpty() && stack.pop() == '(') {
                    count++;
                }
            }
        }
        return count*2;
    }
}
```



但是遇到了用例

```
输入：
"()(()"
输出：
4
预期结果：
2
```

说明, 中间的子串被中间的 `(` 拆散了. 后面的不计数或者说重新计数.





#### Code





​			





