#### Question [面试题 16.26. 计算器](https://leetcode-cn.com/problems/calculator-lcci/)

tag#字符串# #栈# 



#### Description

```
给定一个包含正整数、加(+)、减(-)、乘(*)、除(/)的算数表达式(括号除外)，计算其结果。

表达式仅包含非负整数，+， - ，*，/ 四种运算符和空格  。 整数除法仅保留整数部分。

示例 1:

输入: "3+2*2"
输出: 7
示例 2:

输入: " 3/2 "
输出: 1
示例 3:

输入: " 3+5 / 2 "
输出: 5
说明：

你可以假设所给定的表达式都是有效的。
请不要使用内置的库函数 eval。
```



​		

#### Analysis

已知, 目标对象是一个字符串, 表达式字符串.

表达式中不包含括号, 只有最基本的四则运算.

还有空格.

补充: `Character` 可以判断一个字符是否是数字. 不是的话也可以做(写一个方法, 匹配 0 ~ 9 的 ascii 码值 **0 ~ 9 的 ascii 码值等于数值本身**).

1.用一个栈始终保存可以最后累加的数字.

1.如果是数字的话, 首先累加, 用 num 保存起来, 如果接着的下一个也是数字, 可以进位, 

`num = num*10 + num`. 这样就可以将连续的数字处理成整数值了.

如果是别的运算符的话, 会自动匹配别的. 

2.如果是符号的话, 至少可以确认不是数字, 只能从 +-*/ 中选. 可以拿一个变量转专门保存该字符.

具体可以分情况:

如果遇到的是加号, 将前面的数字放进栈里面. 

如果是减号, 由于最后放的都是直接拿出累加的, 减去一个数相当于加上这个数的负数, 所以改放这个数的负数. - num.

如果是乘号, 说明前一个数字是这个操作数, 第一从栈中给它拿出来, 接着乘上当前值后再将结果放回去, 充当最后可以直接累加的子项.

如果是除号, 同理, 不过这时候就是从栈里拿出来的数做被除数.

每一轮运算符的处理后记得把当前数字归零. 

运算符可以置为空.



最后就是将栈里的数字一个一个 pop 出来累加收获成果了.



#### Code

```java
class Solution {
    //  使用栈, 每次保存可以子运算的结果, 放入栈中, 最后一一累加
    public int calculate(String s) {
        Stack<Integer> stack = new Stack<>();
        char opt = '+';
        int num = 0;

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);

            if (Character.isDigit(c))
                num = num * 10 + (c - '0');
            if ((!Character.isDigit(c) && c != ' ') || i == s.length() - 1) {
                if (opt == '+')
                    stack.push(num);
                else if (opt == '-')
                    stack.push(-num);
                else if (opt == '*')
                    stack.push(stack.pop() * num);
                else    
                    stack.push(stack.pop() / num);
                num = 0;
                opt = c;
            }
        }

        int res = 0;
        while (! stack.isEmpty())
            res += stack.pop();
        return res;
    }
}
```





​			





