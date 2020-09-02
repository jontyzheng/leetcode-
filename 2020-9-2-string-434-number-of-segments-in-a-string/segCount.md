#### Question [434. 字符串中的单词数](https://leetcode-cn.com/problems/number-of-segments-in-a-string/)[Number of Segments in a String](https://leetcode-cn.com/problems/number-of-segments-in-a-string/)

tag#string#



#### Description

```
统计字符串中的单词个数，这里的单词指的是连续的不是空格的字符。

请注意，你可以假定字符串里不包括任何不可打印的字符。

示例:

输入: "Hello, my name is John"
输出: 5
解释: 这里的单词是指连续的不是空格的字符，所以 "Hello," 算作 1 个单词。
```



#### Analysis

题目分析: 这里的单词不是字母组成的字符串, 也不是有字母和符号组成的字符串, 而是连续的字符串.

解题分析: 见答案.

**这里的单词是指**连续的不是空格的字符，所以 "**Hello,**" 算作 1 个单词。[按空格拆字符串挑战]



#### Code

效果:

```
执行结果：
通过
显示详情
执行用时：
0 ms, 在所有 Java 提交中击败了100.00%的用户
内存消耗：
37.4 MB, 在所有 Java 提交中击败了67.20%的用户
```



```
class Solution {
    public int countSegments(String s) {
        int segCount = 0;
        for (int i = 0; i < s.length(); i++) {
            //  I: 当前位不为空格 && 第一位
            //  II: 当前为不为空格 && 前一位为空格的
            if ((i == 0 || s.charAt(i-1) == ' ') && s.charAt(i) != ' ')
                segCount ++;
        }
        return segCount;
    }
}
```

> 将图示情况分成了两种情况 ( - 表示非空格)
>
> - x--- (起始位)
> - --x (其它的位置)
>
> 也就是说, 第一位不为空格的时候加一;
>
> 其他位置当前位置不为空格且前一位也不为空格的时候也加一.



commit 1

```java
class Solution {
    public int countSegments(String s) {
        if (s.length() == 0)
            return 0;
        if (s.length() == 1)
            return 1;
        String[] str = s.split(" ");        
        return str.length;
    }
}
```

**20 / 27** 个通过测试用例

测试用例分析:

```
执行结果：
解答错误
显示详情
输入：
", , , ,        a, eaefa"
输出：
13
预期结果：
6
```

> 题目要求: 
>
> **这里的单词是指**连续的不是空格的字符，所以 "**Hello,**" 算作 1 个单词。[按空格拆字符串挑战]

难点:

> 在将这个测试用例放到代码调试中, 发现, 原字符串的长度为 **23**
>
> 中间有 **8** 个空格.
>
> 而按照 split(" ") split 后, 将得到的数组换行输出后发现
>
> 输出有 13 项:
>
> 除了看得见的 6 项   `,`  `,` `,` `,`  `a,`  `eaefa`  
>
> 还有 7 行是空白的.
>
> 这说明了 2 个问题:
>
> 1. 空格属于字符, 也占字符长度.
> 2. 中间的 8 个空格被当作 7 个项被 split 了出来.
>
> 目前的分析就到这了, 答案还不是很理解.





