#### Question [面试题 01.01. 判定字符是否唯一](https://leetcode-cn.com/problems/is-unique-lcci/)

tag#面试宝典# #字符串# #重复#



#### Description

```
实现一个算法，确定一个字符串 s 的所有字符是否全都不同。

示例 1：

输入: s = "leetcode"
输出: false 
示例 2：

输入: s = "abc"
输出: true
限制：

0 <= len(s) <= 100
如果你不使用额外的数据结构，会很加分。
```



#### Analysis

一开始想到用集合类的 api 的念头给最后一句打消了。。



排序, 将所有可能重复出现的字母放在一块验重.



#### Code

```java
class Solution {
    // 执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
    // 内存消耗：35.9 MB, 在所有 Java 提交中击败了97.01%的用户
    public boolean isUnique(String astr) {
        boolean isUnique = true;
        int len = astr.length();
        if (len == 0 || len == 1)
            return true;
        char[] arr = astr.toCharArray();
        Arrays.sort(arr);
        for (int i=0; i<len; i++) {
            if (i <= len-2) {
                if (arr[i] == arr[i+1]) {
                    isUnique = false;
                    break;
                }
            } else {
                if (arr[i] == arr[i-1]) {
                    isUnique = false;
                    break;
                }
            }            
        }
        return isUnique;
    }
}
```







