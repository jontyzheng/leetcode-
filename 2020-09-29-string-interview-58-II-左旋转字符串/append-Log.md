#### Question  [剑指 Offer 58 - II. 左旋转字符串](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

tag#剑指 offer# #string#



#### Description

```
字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

 

示例 1：

输入: s = "abcdefg", k = 2
输出: "cdefgab"
示例 2：

输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"
 

限制：

1 <= k < s.length <= 10000
```



#### Analysis

利用两个 **StringBuilder**, 一个追加 `n` 前面部分, 另一个追加后半部分, 最后后半部分再追加前半部分.



#### Code

```java
class Solution {
    public String reverseLeftWords(String s, int n) {
        // 执行用时：5 ms, 在所有 Java 提交中击败了23.74%的用户
        // 内存消耗：38.9 MB, 在所有 Java 提交中击败了53.10%的用户
        int len = s.length();
        StringBuilder sbu1 = new StringBuilder();
        StringBuilder sbu2 = new StringBuilder();
        int x = 0;
        while (x < n) {
            sbu1.append(s.charAt(x));
            x++;
        }
        while (n < len) {
            sbu2.append(s.charAt(n));
            n++;
        }
        return sbu2.append(sbu1.toString()).toString();
    }
}
```





