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





#### Code

评论区大佬

```java
public String reverseWords(String s) {
        //将传进来的字符串以空格拆分
        String[] strings = s.trim().split(" ");
        StringBuffer stringBuffer = new StringBuffer();
        //从尾巴开始遍历
        for (int i = strings.length - 1; i >= 0; i--) {
            if (strings[i].equals("")) {
                continue;
            }
            //到头了，append然后去空格
            if (i == 0) {
                stringBuffer.append(strings[i].trim());
            } else {
                // 怕有多余的空格，去掉，再加上去
                stringBuffer.append(strings[i].trim()).append(" ");
            }
        }
        //输出String 完事，安排！
        return stringBuffer.toString();
    }
```



commit 1

```java
class Solution {
    public String reverseWords(String s) {      
        // 输入："a good   example" 
		// 输出："example   good a" 
		// 预期结果："example good a"
        String[] newStr = s.split(" ");
        int len = newStr.length;
        StringBuilder sbuRes = new StringBuilder();
        for (int i=0; i<len; i++) {
            if (i != len-1) {
                StringBuilder sbu = new StringBuilder(newStr[i]);
                sbuRes.append(" ").append(sbu.reverse());     
            }
            else {
                StringBuilder sbu = new StringBuilder(newStr[i]);
                sbuRes.append(sbu.reverse().toString());
            }                 
        }         
        return sbuRes.reverse().toString();
    }
}
```







