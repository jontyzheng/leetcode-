#### Question [125. 验证回文串](https://leetcode-cn.com/problems/valid-palindrome/)

tag#字符串# #StringBuilder# #回文#



#### Description

```
给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

说明：本题中，我们将空字符串定义为有效的回文串。

示例 1:

输入: "A man, a plan, a canal: Panama"
输出: true
示例 2:

输入: "race a car"
输出: false

```



#### Analysis

如果知道 StringBuilder 有一个 reverse 的 api 这道题就十分吃香了.

已知, 回文字符串只考虑字母**和数字**. 字母不分大小写. 说明 a 相当于 A, A 相当于 a.

但是实际相比的时, 又是比较它们的 ascii 码值. 利用 String 的 toLowerCase 可将字符串中含有的一切大写字母转换成小写字母, 其它字符不受影响. "忽略大小写"的问题, 解决.

已知前面的 StringBuilder 的超便利 api, 就可以开始了.

还有一个技巧注意, 就是条件追加的时候, 字符参与运算和 ascii 码值参与运算是一样的. 知道字面字符可以参与其实可以另外记它们的 ascii 码值范围.



#### Code

```java
class Solution {
    // 执行用时：5 ms, 在所有 Java 提交中击败了49.88%的用户
    // 内存消耗：38.4 MB, 在所有 Java 提交中击败了98.20%的用户
    public boolean isPalindrome(String s) {
        if (s == null)  
            return true;
        s = s.toLowerCase();
        int l = s.length();
        StringBuilder sbu = new StringBuilder(l);
        for (char c:s.toCharArray()) {
            if ((c >= '0' && c <= '9') || (c >= 'a' && c <= 'z')) {
                sbu.append(c);
            }
        }
        return sbu.toString().equals(sbu.reverse().toString());
    }
}
```



看到转小写化简的时候吓飞我了.



