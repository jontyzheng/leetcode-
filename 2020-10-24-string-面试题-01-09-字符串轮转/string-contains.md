#### Question [面试题 01.09. 字符串轮转](https://leetcode-cn.com/problems/string-rotation-lcci/)

tag#面试# #字符串# #旋转#



#### Description

```
字符串轮转。给定两个字符串s1和s2，请编写代码检查s2是否为s1旋转而成（比如，waterbottle是erbottlewat旋转后的字符串）。

示例1:

 输入：s1 = "waterbottle", s2 = "erbottlewat"
 输出：True
示例2:

 输入：s1 = "aa", s2 = "aba"
 输出：False
提示：

字符串长度在[0, 100000]范围内。
说明:

你能只调用一次检查子串的方法吗？
```



#### Analysis

题目要求是验证, 两个字符串是否互为反序列.

第一想到的就是**栈**: 

1.拿其中一个字符串拆成字符, 压栈再 pop, 得到其反转字符串, 

2.再和另外一个字符串比较是否相等.

可就怎么都通过不了这个用例:

```
执行结果：
解答错误
显示详情
输入：
""
""
输出：
false
预期结果：
true
```



当然, 要是知道 String 和集合类一样有 contains(s) 的 api 就更好办了.



#### Code

```java
class Solution {
    // 执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
    // 内存消耗：38.1 MB, 在所有 Java 提交中击败了96.25%的用户
    public boolean isFlipedString(String s1, String s2) {
        if (s1.length() != s2.length())
            return false;
        String newStr = s2 + s2;
        return newStr.contains(s1);
    }
}
```





上一次 commit

```java
class Solution {
    public boolean isFlipedString(String s1, String s2) {
                
        Stack<Character> stack = new Stack<>();
        boolean isFlipedString = true;
        int len1 = s1.length();
        int len2 = s2.length();                                                   

        if (len1 != len2) 
            return false;
        if (len1 == 1 && len2 == 1 && s1.equals(s2) && s1 == "")
            return true;

        else {
             for (char e : s1.toCharArray())       
                stack.push(e);
            
            StringBuilder sbu = new StringBuilder();
            while (!stack.isEmpty()) {
                char c = stack.pop();
                sbu.append(c);
            }
            if (sbu.toString().equals(s2))
                isFlipedString = false;
        }       
        return isFlipedString;
    }
}
```

那个差一点点的字符串.



##### 随记

其实还可以试试双指针反方向边走便比较的思路.



