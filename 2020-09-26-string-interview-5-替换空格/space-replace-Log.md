#### Question [替换空格](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)

tag#剑指 offer# #string#



#### Description

```
请实现一个函数，把字符串 s 中的每个空格替换成"%20"。


示例 1：

输入：s = "We are happy."
输出："We%20are%20happy."
 

限制：

0 <= s 的长度 <= 10000
```



#### Analysis

利用 sbu 的条件追加.



#### Code

```java
class Solution {
    public String replaceSpace(String s) {
        // 执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
        // 内存消耗：36.7 MB, 在所有 Java 提交中击败了51.09%的用户
        StringBuilder sbu =  new StringBuilder();
        int len = s.length();
        for (int i=0; i < len; i++) {
            char x = s.charAt(i);
            if (x == ' '){
                sbu.append("%20");                
            } else {
                sbu.append(x);   
            }                 
        }
        return sbu.toString();
    }
}
```







