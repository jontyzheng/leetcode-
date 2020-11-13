#### Question [1221. 分割平衡字符串](https://leetcode-cn.com/problems/split-a-string-in-balanced-strings/)

tag##



#### Description

```
在一个「平衡字符串」中，'L' 和 'R' 字符的数量是相同的。

给出一个平衡字符串 s，请你将它分割成尽可能多的平衡字符串。

返回可以通过分割得到的平衡字符串的最大数量。

 

示例 1：

输入：s = "RLRRLLRLRL"
输出：4
解释：s 可以分割为 "RL", "RRLL", "RL", "RL", 每个子字符串中都包含相同数量的 'L' 和 'R'。
示例 2：

输入：s = "RLLLLRRRLR"
输出：3
解释：s 可以分割为 "RL", "LLLRRR", "LR", 每个子字符串中都包含相同数量的 'L' 和 'R'。
示例 3：

输入：s = "LLLLRRRR"
输出：1
解释：s 只能保持原样 "LLLLRRRR".
 

提示：

1 <= s.length <= 1000
s[i] = 'L' 或 'R'
分割得到的每个字符串都必须是平衡字符串。

```



#### Analysis

##### 【浓缩版】

想要确保分割出来的子串中两个字母的数量相等, 就相当于一个栈先压后弹然后栈刚好为空一样.



##### 【详细版】

平衡字符串的定义: 

已知给定的字符串一定只有 `L` 和 `R` 两个字母构成, 并且它们的在数量上都是相等的.

现在问: 如何将它们分割, 分割出来的子串中, `L` 和 `R` 的数量相等?

1.工具: 很自然联想到栈. 和平衡字符串的问题类似.

2.字符串并不是固定先 L 后 R 出现的, 也有可能 R 先出现, 所以压栈的条件:

2.1.应该以栈是否为空为标准: 如果为空的话无脑添加.

2.2.如果栈中有数据(等待匹配), 下一个如果和里面的相同, 也是继续压入栈中的.

> (L	-	L?

2.3.如果栈中有数据, 而下一个和里面的不相同, 说明过来的是请求匹配的. 这时候出一个表示匹配成功.

3.每次栈为空, 匹配成功时, 计数一次.

得到的总计数器值, 就是连续匹配的可能次数.



#### Code

```java
class Solution {
    //执行用时：4 ms
    public int balancedStringSplit(String s) {
        if (s.length() == 1)
            return 0;
        Stack<Character> stack = new Stack<>();
        int emptyCount = 0;
        for (char c : s.toCharArray()) {
            if (stack.isEmpty()) 
                stack.push(c);
            else if (!stack.isEmpty() && stack.peek() != c) {                 
                stack.pop();
                if (stack.isEmpty())
                    emptyCount++;            
            }
            else if (!stack.isEmpty() && stack.peek() == c) {
                stack.push(c);
            }
        }
        return emptyCount;
    }
}
```



​			

##### 【本题小结】

先了解平衡字符串是什么, 题目要求分割的要求是什么(分割出去的部分, L 和 R 数量相等 则视为一次良好的分割).

分割匹配的次数就是栈匹配完成清空的次数.	





