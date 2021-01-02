#### Question [1317. 将整数转换为两个无零整数的和](https://leetcode-cn.com/problems/convert-integer-to-the-sum-of-two-no-zero-integers/)

tag#数学# #字符串# 



#### Description

```
「无零整数」是十进制表示中 不含任何 0 的正整数。

给你一个整数 n，请你返回一个 由两个整数组成的列表 [A, B]，满足：

A 和 B 都是无零整数
A + B = n
题目数据保证至少有一个有效的解决方案。

如果存在多个有效解决方案，你可以返回其中任意一个。

 

示例 1：

输入：n = 2
输出：[1,1]
解释：A = 1, B = 1. A + B = n 并且 A 和 B 的十进制表示形式都不包含任何 0 。
示例 2：

输入：n = 11
输出：[2,9]
示例 3：

输入：n = 10000
输出：[1,9999]
示例 4：

输入：n = 69
输出：[1,68]
示例 5：

输入：n = 1010
输出：[11,999]
 

提示：

2 <= n <= 10^4

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/convert-integer-to-the-sum-of-two-no-zero-integers
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```







#### Code

```java
class Solution {
    //执行用时：1 ms
    public int[] getNoZeroIntegers(int n) {
        //  利用 String 的 contains()
        int i = 1;
        int j = n - 1;
        while (true) {
            if (String.valueOf(i).contains("0") == false && String.valueOf(j).contains("0") == false) {
                return new int[]{i, j};
            }
            i += 1;
            j = n - i;
            //  继续下一轮
        }
    }
}
```







#### 分析

题目的概念:

无零整数, 各个位上的数字不为 `0` 的数字.

现给定一个整数, 要将它拆成两个无零整数, 然后返回给它.

> 1.返回结果一定是 2 个元素的整型数组.
>
> 2.已知给定的数字一定存在这样的解.
>
> 3.返回任意一组, 只要返回要求即可.

已知, 字符串存在一个方法 `contains("xx")` 

如果, 可以获得目标数字对应的字符串, 就可以直接判断出加数当中是否还有位数为 `0` 的了.



方法:

1.先通过 String.valueOf(xxx) 获取数字/字符对应的字符串.

2.使用 contains() 判断数字中是否含有 0 的字符.

3.如果有, 则让其中一个加数减一(另一个加数同步变化), 继续判断, 直到两个加数正好达到条件. 即可返回.



#### 测试用例过滤



###### I.排除一些像 11, 21 的情况

```java
class Solution {
    public int[] getNoZeroIntegers(int n) {
        int[] sumpair = new int[2];
        if (n/10 != 1) {
            return new int[]{1, n-1};
        }
        return sumpair;
    }
}
```



> ```
> 149 / 206 个通过测试用例
> 
> 输入：
> 11
> 输出：
> [0,0]
> 预期：
> [2,9]
> ```
>
> 还应该考虑刚好个位数上不为 0 的个数.



###### II.发现了"并不是个数才有可能为 0"

```java
class Solution {
    public int[] getNoZeroIntegers(int n) {
        //int[] sumpair = new int[2];
        //  只要不是刚好比10的倍数多 1, 1 和差都可以满足条件
        if (n/10 != 1) {
            return new int[]{1, n-1};
        }
        else {
            return new int[]{2, n-2};
        }        
    }
}
```



> ```
> 149 / 206 个通过测试用例
> 
> 输入：
> 1010
> 输出：
> [1,1009]
> 预期：
> [11,999]
> ```
>
> 说明: 位数为 0 的不是只有个位数.



#### 讲讲你一开始的想法

一开始看到关键词只要返回任意一组, 就说明题目的满足条件的情形应该是十分多的, 只要返回其中一个即可.

首先想到的就是 {1, n-1}.

最不费力的情况.

但是有可能, 出现 11, 101 这样的减去 1之后刚好等于 10 的情况, 这时候继续减去一个 1 就可以.

但是像 101 这样的, 减去后, 其它位数还存在 0, 就想:

> 难道要对每一位数字取下来, 对 10 整数判断吗?
>
> 那工程该多大阿?

然后就看到了解答.

用 String 的 `valueOf` 方法就可以获取到整数值对应的字符串形式, 用 contains 就方便了.





#### 本期leetcode	

回顾字符串对整数的一个处理方法 `valueOf`

数学 tag 的也可能和字符串有关.

