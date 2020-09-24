#### Question [斐波那契数列](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/)

tag#剑指offer# #math#



#### Description

```
写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项。斐波那契数列的定义如下：

F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

 

示例 1：

输入：n = 2
输出：1
示例 2：

输入：n = 5
输出：5
 

提示：

0 <= n <= 100
```



#### Analysis

**根据斐波那契数列的定义去计算就可以了**.



#### Code

```java
class Solution {
    public int fib(int n) {
        //  0, 1, 1, 2, 3, 5
        int former = 0;
        int later = 1;
        int result = 1;
        if (n <= 1) 
            return n;    
        for (int i=2; i<=n; i++) {
            result = (former + later)%1000000007;
            former = later;
            later = result;
        }
        return result;
    }
}
```

运行效果:

执行结果：

通过

显示详情

执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户





数值超模的时候%模就可以了. 

(数值在模范围内, 总是不变, 在范围外的, 超过多少就会取超出的多少)

```java
result = (former + later)%1000000007;
```

