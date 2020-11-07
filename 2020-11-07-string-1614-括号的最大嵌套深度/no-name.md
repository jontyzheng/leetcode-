#### Question [1614. 括号的最大嵌套深度](https://leetcode-cn.com/problems/maximum-nesting-depth-of-the-parentheses/)

tag##



#### Description

```
如果字符串满足一下条件之一，则可以称之为 有效括号字符串（valid parentheses string，可以简写为 VPS）：

字符串是一个空字符串 ""，或者是一个不为 "(" 或 ")" 的单字符。
字符串可以写为 AB（A 与 B 字符串连接），其中 A 和 B 都是 有效括号字符串 。
字符串可以写为 (A)，其中 A 是一个 有效括号字符串 。
类似地，可以定义任何有效括号字符串 S 的 嵌套深度 depth(S)：

depth("") = 0
depth(C) = 0，其中 C 是单个字符的字符串，且该字符不是 "(" 或者 ")"
depth(A + B) = max(depth(A), depth(B))，其中 A 和 B 都是 有效括号字符串
depth("(" + A + ")") = 1 + depth(A)，其中 A 是一个 有效括号字符串
例如：""、"()()"、"()(()())" 都是 有效括号字符串（嵌套深度分别为 0、1、2），而 ")(" 、"(()" 都不是 有效括号字符串 。

给你一个 有效括号字符串 s，返回该字符串的 s 嵌套深度 。

 

示例 1：

输入：s = "(1+(2*3)+((8)/4))+1"
输出：3
解释：数字 8 在嵌套的 3 层括号中。
示例 2：

输入：s = "(1)+((2))+(((3)))"
输出：3
示例 3：

输入：s = "1+(2*3)/(2-1)"
输出：1
示例 4：

输入：s = "1"
输出：0
 

提示：

1 <= s.length <= 100
s 由数字 0-9 和字符 '+'、'-'、'*'、'/'、'('、')' 组成
题目数据保证括号表达式 s 是 有效的括号表达式
```



#### Analysis

题目看着很长, 实际上描述的问题十分简单 - 

给出的是一个规则的带括号表达式. 其它字符可以忽略不记.

![](https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-11-07-string-1614-%E6%8B%AC%E5%8F%B7%E7%9A%84%E6%9C%80%E5%A4%A7%E5%B5%8C%E5%A5%97%E6%B7%B1%E5%BA%A6/cnt-continuous-(.jpg)

假如这样一道例子放在你面前, 你会怎么计算它?

> 答: 我会从左往右计数 `(`  主要指找"连续最多的 `(` , 不如说是没有被 `)` 拆散的 连续 `(` ".
>
> 我会每遇到一个 `(` 就计数加 1. 
>
> 随即记录已经遇到的 `(`  个数, 确保是当前遇到最大的括号数.
>
> 有括号合上了, 就减掉. 继续接着上一个括号计数.
>
> 当然了, 这里说的"括号"指的都是做左括号.



#### Code

```java
class Solution {
    public int maxDepth(String s) {
		int depth = 0;
        int tmp = 0;
        for (char c : s.toCharArray()) {
            if ( c == '(' ) {
                tmp++;
                depth = Math.max(tmp, depth);
            }
            else if ( c == ')' )
                tmp--;
        }
        return depth;
    }
}
```

