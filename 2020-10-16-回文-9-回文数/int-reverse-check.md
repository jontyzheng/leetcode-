#### Question [9. 回文数](https://leetcode-cn.com/problems/palindrome-number/)

tag#剑指# #回文# 



#### Description

```
判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

示例 1:

输入: 121
输出: true
示例 2:

输入: -121
输出: false
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。
示例 3:

输入: 10
输出: false
解释: 从右向左读, 为 01 。因此它不是一个回文数。
进阶:

你能不将整数转为字符串来解决这个问题吗？

```



#### Analysis

进位移动, 可以用另外一个值从 0 开始累加掉下来的值.

btw, 记住, 最后的结果是要与初始值比较的. 

如果过程中有对参数进行更新的话, 要不提前对初始值拷贝一份, **对副本操作**, 最后和原变量比对. 

要不提前拷贝一份, 对变量就地操作, 最后和提前拷贝的副本比较.

#### Code

```java
class Solution {
    public boolean isPalindrome(int x) {        
        //  依题意可得, 负数可以直接排除
        if (x<0)
            return false;
        int y = 0;
        //  最后一步与原值比较是否回文, 必须提前保证原值有一份拷贝
        int copyed = x;
        while (x!=0) {
            int temp = x%10;
            y = y*10 + temp;
            x = x/10;
        }
        return copyed==y;
    }
}
```







