#### Question [859. 亲密字符串](https://leetcode-cn.com/problems/buddy-strings/)

tag#string#



#### Description

```
给定两个由小写字母构成的字符串 A 和 B ，只要我们可以通过交换 A 中的两个字母得到与 B 相等的结果，就返回 true ；否则返回 false 。

 

示例 1：

输入： A = "ab", B = "ba"
输出： true
示例 2：

输入： A = "ab", B = "ab"
输出： false
示例 3:

输入： A = "aa", B = "aa"
输出： true
示例 4：

输入： A = "aaaaaaabc", B = "aaaaaaacb"
输出： true
示例 5：

输入： A = "", B = "aa"
输出： false
 

提示：

0 <= A.length <= 20000
0 <= B.length <= 20000
A 和 B 仅由小写字母构成。
```



#### Analysis

题意分析: 亲密字符串的定义 - 两个字符串有且只有两个字符不相等但交换后可以相等, 那么它们就互为亲密字符串. 

由给出的例子可知: 长度为 2 且有同一个字符组成的字符串的除外 (ab ab).





#### Code

commit 1

优先排除一些特殊情况后, 循环遍历 A 和 B, 找不相同的字符, 如果最后找到 2 个则说明"符合"**刚好只需交换两次变相等**的情况.

效果: **21 / 29** 个通过测试用例

```java
class Solution {
    public boolean buddyStrings(String A, String B) {
        int lenA = A.length();
        int lenB = B.length();
        if (lenA == 0 || lenB == 0 || lenA != lenB)
            return false;
        if (A.equals(B) && lenA == 2 && A.charAt(0) == A.charAt(1))
            return true;
        if (A.equals(B) && lenA == 2 && A.charAt(0) != A.charAt(1))
            return false;        
        char[] arrA = A.toCharArray();
        char[] arrB = B.toCharArray();            
        int len = arrA.length;
        int count = 0;
        for (int i = 0; i < len; i++) {
            if (arrA[i] != arrB[i])
                count++;
        }        
        return count == 2;
    }
}
```

实际效果:

```
执行结果：
解答错误
显示详情
输入：
"abcaa"
"abcbb"
输出：
true
预期结果：
false
```

> **新的情况**: 有两个不相等但是这两个不一定是来自同两个字符
>
> 把这两个不同的字符记录下来, 交叉比较判等



commit 2

通过参考评论区的优秀答案, 有了 "将原字符串就地交换后判断等" 的思路.

效果: **20 / 29** 个通过测试用例

```java
class Solution {
    public boolean buddyStrings(String A, String B) {
        int lenA = A.length();
        int lenB = B.length();
        if (lenA == 0 || lenB == 0 || lenA != lenB)
            return false;
        if (A.equals(B) && lenA == 2 && A.charAt(0) == A.charAt(1))
            return true;          
        char[] arrA = A.toCharArray();
        char[] arrB = B.toCharArray();            
        int len = arrA.length;
        //  换成字符数组的题
        if (len == 2 && arrA[0] == arrB[1] && arrB[1] == arrA[0])           
            return true;
        int count = 0;        
        for (int i = 0; i < len; i++) {
            if (arrA[i] != arrB[i])                
                count++;
                char c;
                c = arrB[i];
                arrB[i] = arrA[i];
                arrA[i] = c;
        }   
        return count ==  2 && arrA == arrB;        
    }
}
```

测试用例分析:

```
执行结果：
解答错误
显示详情
输入：
"aaaaaaabc"
"aaaaaaacb"
输出：
false
预期结果：
true
```

> 同一种情况
>
> 可能原因: 没有交换成功.

commit 3

> 

```java
class Solution {
    public boolean buddyStrings(String A, String B) {
        int lenA = A.length();
        int lenB = B.length();
        //  亲密字符串的基本条件: 长度相等, 任何一个都不为 0
        if (lenA == 0 || lenB == 0 || lenA != lenB)
            return false;
        //  aa aa 的特殊情况
        if (A.equals(B) && lenA == 2 && A.charAt(0) == A.charAt(1))
            return true;          
        char[] arrA = A.toCharArray();
        char[] arrB = B.toCharArray();            
        int len = arrA.length;
        //  换成字符数组的题
        if (len == 2 && arrA[0] == arrB[1] && arrB[1] == arrA[0])           
            return true;
        int count = 0;   
        //  一般情况     
        for (int i = 0; i < len; i++) {
            if (arrA[i] != arrB[i])                
                count++;
                char c;
                c = arrB[i];    //  当前位赋值给 c
                arrB[i] = arrA[i];  //  交换单边的值
                arrA[i] = c;    //  完成交换
        }   
        return count ==  2 && Arrays.equals(arrA, arrB);        
    }
}
```

测试用例分析:

```
输入：
"aaaaaaabc"
"aaaaaaacb"
输出：
false
预期：
true
```

> 放弃



