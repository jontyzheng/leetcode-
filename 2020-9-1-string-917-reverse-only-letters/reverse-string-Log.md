#### Question [917. 仅仅反转字母](https://leetcode-cn.com/problems/reverse-only-letters/)/[Reverse Only Letters](https://leetcode-cn.com/problems/reverse-only-letters/)

tag#string#



#### Description

```
给定一个字符串 S，返回 “反转后的” 字符串，其中不是字母的字符都保留在原地，而所有字母的位置发生反转。

 

示例 1：

输入："ab-cd"
输出："dc-ba"
示例 2：

输入："a-bC-dEf-ghIj"
输出："j-Ih-gfE-dCba"
示例 3：

输入："Test1ng-Leet=code-Q!"
输出："Qedo1ct-eeLg=ntse-T!"
 

提示：

S.length <= 100
33 <= S[i].ASCIIcode <= 122 
S 中不包含 \ or "
```





#### Analysis

题意分析: 给定一个字符串, 字符串中除了字母还会有其它的字符. 现要将其中的字母反转, 并返回反转后的字符串. 如 `ab-cd` 返回 `dc-ba`.

解题分析: 这道题没什么好说的, 双指针定位, 在两头都遍历到字母的时候进行字符对调. 当然, 原字符串需要转化为字符数组.

判断一个字符是不是字母时, 可以用 Character 的 `+ isLetter(char c): boolean`. 比范围比较简单得多. 虽然大写字母的码表范围为 **65**-90, 小写的是从 **97**-122.



#### Code

```java
class Solution {
    public String reverseOnlyLetters(String s) {
        char[] chars = s.toCharArray();
        int sIndex = 0, eIndex = chars.length - 1;
        while (sIndex < eIndex) {
            if (!Character.isLetter(chars[sIndex])) {
                sIndex++;
            }
            if (!Character.isLetter(chars[eIndex])) {
                eIndex--;
            }
            if (Character.isLetter(chars[sIndex]) &&
                    Character.isLetter(chars[eIndex])) {
                char temp = chars[sIndex];
                chars[sIndex] = chars[eIndex];
                chars[eIndex] = temp;
                sIndex++;
                eIndex--;
            }
        }
        return new String(chars);
    }
}
```

> 👆 评论区好答案:
>
> 只有遇到字母的时候才移动 `i` `j` 指针 - 如果不是字母的话就移动, 只有 `i` 和 `j` 都遇到字母的时候才移动.
>
> 这种方法把这两个变化分开独立了. `i++` 和 `j--` 都独立放在各自的方法体里面. 不会随着外层循环的变化而变动. 互不影响又有达到了只有同时遇到字母时才进行. 不会有一边遇到, 一边没有遇到的情况.



commit 1

> 按照思路写的第一次代码. 提示随后一行编译错误. 无解.

```java
class Solution {
    public String reverseOnlyLetters(String S) {
        char[] chars = S.toCharArray();
        int len = arr.length;
        if (len < 0)
            return null;
        if (len == 1)
            return S;        
        for (int i = 0, j = len-1; i <= len/2 && j >= len/2+1 &&
            ((chars[i] > 60 && chars[i] < 90) || (chars[i] > 97 && chars[i] < 122)) && 
            ((chars[j] > 60 && chars[j] < 90) || (chars[j] > 97 && chars[j] < 122));
            i++, j--) {                                                                        
                char c;
                c = chars[i];
                chars[i] = chars[j];
                chars[j] = c;
            }            
        }        
        return new String(arr);
    }
}
```

> 缺点: `i` 和 `j` 是同步变化的. for 循环里的双指针只能是同步变化.
>
> 没有遇到字母的时候或者一头遍历到, 一头没遍历到也是同步变化. 会跳过部分情况.



