#### Question [1281. 整数的各位积和之差](https://leetcode-cn.com/problems/subtract-the-product-and-sum-of-digits-of-an-integer/)

tag##



#### Description

```
给你一个整数 n，请你帮忙计算并返回该整数「各位数字之积」与「各位数字之和」的差。

 

示例 1：

输入：n = 234
输出：15 
解释：
各位数之积 = 2 * 3 * 4 = 24 
各位数之和 = 2 + 3 + 4 = 9 
结果 = 24 - 9 = 15
示例 2：

输入：n = 4421
输出：21
解释： 
各位数之积 = 4 * 4 * 2 * 1 = 32 
各位数之和 = 4 + 4 + 2 + 1 = 11 
结果 = 32 - 11 = 21
 

提示：

1 <= n <= 10^5

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/subtract-the-product-and-sum-of-digits-of-an-integer
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```







#### Code

```java
class Solution {
    //执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户    
    public int subtractProductAndSum(int n) {
        int multifyRes = 1;
        int sumRes = 0;
        boolean hasZero = false;
        while (n > 0) {         //  update: n >= 0 - n > 0
            int x = n%10;       //  update: x 取商数改取余数
            if (x == 0) 
                hasZero = true;
            sumRes += x;
            multifyRes *= x;
            n /= 10;
        }
        return hasZero == true? (-sumRes) : (multifyRes-sumRes);
    }
}
```





#### 分析

典型的按"位"运算



#### 测试用例过滤

###### i

```java
class Solution {
    //超出时间限制
    public int subtractProductAndSum(int n) {
        int multifyRes = 1;
        int sumRes = 0;
        boolean hasZero = false;
        while (n >= 0) {
            int x = n/10;
            if (x == 0) 
                hasZero = true;
            sumRes += x;
            multifyRes *= x;
            n /= 10;
        }
        return hasZero == true? (-sumRes) : (multifyRes);
    }
}
```

> 说明:
>
> while 循环不断指定导致的超时



###### ii

更新: `while(n >=0)` - `while (n >0)`

```java
class Solution {    
    public int subtractProductAndSum(int n) {
        int multifyRes = 1;
        int sumRes = 0;
        boolean hasZero = false;
        while (n > 0) {         //  update: n >= 0 - n > 0
            int x = n/10;       
            if (x == 0) 
                hasZero = true;
            sumRes += x;
            multifyRes *= x;
            n /= 10;
        }
        return hasZero == true? (-sumRes) : (multifyRes-sumRes);
    }
}
```

> 运行
>
> ```
> 输入
> 234
> 输出
> -25
> 预期结果
> 15
> ```
>
> 说明:
>
> 通过调试才知道 x 经过第一次 while 循环体的时候得到是 23
>
> 我们要的是最后一位而不是前两位

###### iii

```java
class Solution {
    //执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户    
    public int subtractProductAndSum(int n) {
        int multifyRes = 1;
        int sumRes = 0;
        boolean hasZero = false;
        while (n > 0) {         //  update: n >= 0 - n > 0
            int x = n%10;       //  update: x 取商数改取余数
            if (x == 0) 
                hasZero = true;
            sumRes += x;
            multifyRes *= x;
            n /= 10;
        }
        return hasZero == true? (-sumRes) : (multifyRes-sumRes);
    }
}
```

> 运行
>
> ```
> 执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户    
> ```
>
> 



#### 讲讲你一开始的想法

按"位"运算是十分常见的题型了

所以看到的时候思路就自然出来了

因为之前也遇到过非方法超时的情况, 最近又在看 while 循环, 所以遇到超时的情况, 想着一共也在 10^5, 说大不大, 可是这样的运算必须至少循环一次拿到每一位的位数呀

于是检查了一下有没有可能是 while 条件的问题.

果然, 当最后一位的时候, n 最后得到 0, 总是满足 while 循环条件, 所以才一直跑.

找到问题, 加上取对数了就行.



#### 本期leetcode	

做多了一道"按位"运算的题目



