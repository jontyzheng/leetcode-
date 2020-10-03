#### Question [剑指 Offer 58 - I. 翻转单词顺序](https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/)

tag#剑指 offer# #string#



#### Description

```
输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student. "，则输出"student. a am I"。

 

示例 1：

输入: "the sky is blue"
输出: "blue is sky the"
示例 2：

输入: "  hello world!  "
输出: "world! hello"
解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
示例 3：

输入: "a good   example"
输出: "example good a"
解释: 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
 

说明：

无空格字符构成一个单词。
输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
```



#### Analysis

由例子可得, 题目是将数组中的字符串顺序颠倒过来. 

```
输入: "the sky is blue"
输出: "blue is sky the"
```

这一点可以从后往前遍历然后追加实现.

如果是去掉单词空格的话, 肯定是要用到 trim. 针对 split 只是按照特定字符 (空格算一个字符) 分离字符串, 如果是连续多个空格的话, 空格也会被当作一个数组项返回. 这一点可以通过在追加前加上一个判定语句来消除这一点.

例子:

SplitTest.java

```java
package com.crazy.string;

/**
 * split(" ") 以一个空格分隔字符串
 * @author Jonty Zheng
 */

public class SplitTest2 {
    public static void main(String[] args) {
        String s = "a good   example";
        String[] res = s.split(" ");
        int i = 0;
        for (String ss:res) {
            System.out.println("第 i 项:" + ss + ",");
            i++;
        }

    }
}

```

运行结果:

```
第 i 项:a,
第 i 项:good,
第 i 项:,
第 i 项:,
第 i 项:example,
```





需要的注意就是最后记得将最后一次追加的空格给"掐头去尾"掉. 当然, 开头也需要. 针对第二个测试用例所示.





#### Code

```java
class Solution {
    public String reverseWords(String s) {
        //执行用时：1 ms, 在所有 Java 提交中击败了100.00%的用户
        //内存消耗：39.1 MB, 在所有 Java 提交中击败了30.20%的用户
        String[] strArr = s.trim().split(" ");
        int len = strArr.length;
        
        StringBuilder resSbu = new StringBuilder();
        for (int i=len-1; i>=0; i--) {
            if (!strArr[i].equals("")) {       //  加一个判断条件
                String ss = strArr[i].trim();   //  将单词前后的空格掐头去尾
                resSbu.append(ss).append(" ");
            }            
        }
        return resSbu.toString().trim();    //  去掉最后一个追加的空格
    }
}
```







