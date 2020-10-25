#### Question [面试题 01.02. 判定是否互为字符重排](https://leetcode-cn.com/problems/check-permutation-lcci/)

tag#面试# #字符串#



#### Description

```
给定两个字符串 s1 和 s2，请编写一个程序，确定其中一个字符串的字符重新排列后，能否变成另一个字符串。

示例 1：

输入: s1 = "abc", s2 = "bca"
输出: true 
示例 2：

输入: s1 = "abc", s2 = "bad"
输出: false
说明：

0 <= len(s1) <= 100
0 <= len(s2) <= 100
```



#### Analysis

假设它们可以通过**重排**可以得到彼此, 那么它们升序后的结果一定相等.



#### Code

```java
class Solution {
    // 执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
    // 内存消耗：35.9 MB, 在所有 Java 提交中击败了97.88%的用户
    public boolean CheckPermutation(String s1, String s2) {
        char[] arr1 = s1.toCharArray();
        char[] arr2 = s2.toCharArray();        
        Arrays.sort(arr1);
        Arrays.sort(arr2);
        StringBuilder sbu1 = new StringBuilder();
        StringBuilder sbu2 = new StringBuilder();
        for (char c : arr1) 
            sbu1.append(c);
        for (char c : arr2)
            sbu2.append(c);
        return sbu1.toString().equals(sbu2.toString());
    }
}
```







