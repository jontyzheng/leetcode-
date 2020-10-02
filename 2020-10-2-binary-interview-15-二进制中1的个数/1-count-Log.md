#### Question [剑指 Offer 15. 二进制中1的个数](https://leetcode-cn.com/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/)

tag#剑指 offer# #binary# 



#### Description

```
请实现一个函数，输入一个整数，输出该数二进制表示中 1 的个数。例如，把 9 表示成二进制是 1001，有 2 位是 1。因此，如果输入 9，则该函数输出 2。

示例 1：

输入：00000000000000000000000000001011
输出：3
解释：输入的二进制串 00000000000000000000000000001011 中，共有三位为 '1'。
示例 2：

输入：00000000000000000000000010000000
输出：1
解释：输入的二进制串 00000000000000000000000010000000 中，共有一位为 '1'。
示例 3：

输入：11111111111111111111111111111101
输出：31
解释：输入的二进制串 11111111111111111111111111111101 中，共有 31 位为 '1'。
```

注意：本题与主站 191 题相同：https://leetcode-cn.com/problems/number-of-1-bits/



#### Analysis

传递一个二进制样子的整数, 虽然对应的十进制是另外一个数字, 但是并不需要转换成十进制, 只需要返回原参数中 1 的个数.

尝试一: 如果可以将参数放到一个数组里就好了, 可以遍历出结果. 然而参数类型是 int 而不是 字符串, 数组.

通过题意的分析, 可以将参数当成一个整数.

如果是整数的话, 对位数上的操作就可以参考力扣的另外一道题 - [7. 整数反转](https://leetcode-cn.com/problems/reverse-integer/) 中的运算, 逐步将各个位数上数字卸货和取数了.



#### Code

用一个变长数组盛放 1 的个数, 然后遇 1 放进, 最后返回 list 的长度.

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
                
        List<Integer> list = new ArrayList<>();
        while (n!=0) {
            int num = n%10;            
            if (num==1) 
                list.add(num);
            n = n/10;
        }
        return list.size();
    }
}
```

> 感觉有戏

```
18 / 601 个通过测试用例
状态：解答错误
提交时间：1 小时前
输入：
00000000000000000000000000001011
输出：
2
预期：
3
```





##### commit 2

> 调试 1011 的话没错, 而 00000000000000000000001010 时就有问题.
>
> 更新: 将参数当作二进制类型, 10 改为 2.
>
> 原来的 list 也不需要了, 用一个 count 计数器即可.

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {            
        int count = 0;
        while (n>0) {
            int num = n%2;     //  取余           
            if (num!=0) {
                count++;
            }                
            n = n/2;           //  小数点左移
        }
        return count;
    }
}
```



> 通过的测试用例明显变多了. 

```
315 / 601 个通过测试用例
状态：解答错误
提交时间：21 分钟前
输入：
11111111111111111111111111111101
输出：
0
预期：
31
```

> 不想了
>
> 自动转换的机制太坑了
>
> 然后, 实际上, 这个测试用例中的参数根据无法作为该方法的参数.
>
> 11111111111111111111111111111101 **根本无法用 int 表示**, 会被当成一个 long 值处理. 然后提醒数值过大. 

![](https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-10-2-binary-interview-15-%E4%BA%8C%E8%BF%9B%E5%88%B6%E4%B8%AD1%E7%9A%84%E4%B8%AA%E6%95%B0/bad-test.jpg)

##### commit 3

> 既然会被当作一个 long 类型处理, 那就将进来的参数强转再来.
>
> 引入一个 long 变量对 n 强转, 继续同样的操作.

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {   
        long x = (long)n;
        int count = 0;
        while (x!=0) {            
            if (x%2!=0) {    //  取余           
                count++;
            }                
            x = x/2;           //  小数点左移
        }
        return count;
    }
}
```

> 通过多了几个测试用例

```
318 / 601 个通过测试用例
状态：解答错误
提交时间：几秒前
输入：
11111111111111111111111111111101
输出：
2
预期：
31
```

> 不想也罢



评论区答案:

```java

```

