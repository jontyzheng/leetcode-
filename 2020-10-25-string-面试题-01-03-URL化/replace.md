#### Question [面试题 01.03. URL化](https://leetcode-cn.com/problems/string-to-url-lcci/)

tag#面试# #字符串# #空格字符处理#



#### Description

```
URL化。编写一种方法，将字符串中的空格全部替换为%20。假定该字符串尾部有足够的空间存放新增字符，并且知道字符串的“真实”长度。（注：用Java实现的话，请使用字符数组实现，以便直接在数组上操作。）

示例1:

 输入："Mr John Smith    ", 13
 输出："Mr%20John%20Smith"
示例2:

 输入："               ", 5
 输出："%20%20%20%20%20"
提示：

字符串长度在[0, 500000]范围内。

```



#### Analysis

字符串的两大 api:

1.截取子串 substring(int start, int end)

2.替换字符串 replace(oldStr, newStr);

当然, 如果忽略题目要求的 "（注：用`Java`实现的话，请使用字符数组实现，以便直接在数组上操作。）" 的话. 这样是最简单的.

那么问题来了, 为什么可以截取 0, length 之间的字符串.



#### Code

```java
class Solution {
    // 执行用时：11 ms, 在所有 Java 提交中击败了87.82%的用户
    // 内存消耗：46.9 MB, 在所有 Java 提交中击败了62.60%的用户
    public String replaceSpaces(String S, int length) {
        S = S.substring(0, length);
        return S.replace(" ", "%20");
    }
}
```







