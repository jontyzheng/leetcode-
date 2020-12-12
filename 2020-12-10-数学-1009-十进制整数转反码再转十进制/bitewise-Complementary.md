#### Question [1009. 十进制整数的反码](https://leetcode-cn.com/problems/complement-of-base-10-integer/)

tag##



#### Description

```
每个非负整数 N 都有其二进制表示。例如， 5 可以被表示为二进制 "101"，11 可以用二进制 "1011" 表示，依此类推。注意，除 N = 0 外，任何二进制表示中都不含前导零。

二进制的反码表示是将每个 1 改为 0 且每个 0 变为 1。例如，二进制数 "101" 的二进制反码为 "010"。

给你一个十进制数 N，请你返回其二进制表示的反码所对应的十进制整数。

 

示例 1：

输入：5
输出：2
解释：5 的二进制表示为 "101"，其二进制反码为 "010"，也就是十进制中的 2 。
示例 2：

输入：7
输出：0
解释：7 的二进制表示为 "111"，其二进制反码为 "000"，也就是十进制中的 0 。
示例 3：

输入：10
输出：5
解释：10 的二进制表示为 "1010"，其二进制反码为 "0101"，也就是十进制中的 5 。
 

提示：

0 <= N < 10^9
本题与 476：https://leetcode-cn.com/problems/number-complement/ 相同

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/complement-of-base-10-integer
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```







#### Code

```java
class Solution {
    //执行用时：1 ms, 在所有 Java 提交中击败了28.43%的用户
    public int bitwiseComplement(int N) {
        String s = Integer.toBinaryString(N);
        int sum = 0;
        //  101    010
        for (char c : s.toCharArray()) {    
            sum <<= 1;        
            if (c == '0')                
                sum += 1;                             
        }
        return sum;
    }
}
```





#### 分析

题目要求的是如何将一个数的二进制取反后, 计算出对应的十进制数值.



题目中有提到几个条件大大节省了题目的难度



i. 0<=N<10^9: 正数的二进制码总是以 1 开头, 得到的总是以 0 开头, 得到的数字一定比原来的数值小.

ii. 没有前导零 不用考虑多余的位数 

iii. 进位: sum += sum*进制 + current





#### 测试用例过滤



##### 讲讲你一开始的想法

```java
class Solution {
    public int bitwiseComplement(int N) {
        String s = Integer.toBinaryString(N);
        int sum = 0;
        for (char c : s.toCharArray()) {            
            if (c == '1')
                sum = sum << 1 + 0;
            else 
                sum = sum << 1 + 1;
        }
        return sum;
    }
}
```

运行

```
输入
5
输出
0
预期结果
2
```

> 一开始的想法是因为它是二进制之间来回运算嘛, 就想到了最近学到的移位运算符.
>
> 题目是从一个数的二进制中, 取反, 然后计算取反后对应的十进制数值.
>
> 计算都可以通过移位运算符解决.
>
> 所以, 遇到 1 就像遇到 0 处理, 遇到 0 就像遇到 1处理.
>
> 遇 1 (变 0)左移
>
> 遇 0 (变 1)左移后加上 1



用例过程解释:

我在 IDE 上调试了一遍 << 移位运算符的用法

发现

0 << 1 = 0			①

0 << 1 + 1 = 0	  ②

这一点很奇怪. 也就是说初始值为 0 的 sum, 经过一次移位还是 0.

于是就继续看具体的实现方法.



##### 更新 II

```java
class Solution {
    public int bitwiseComplement(int N) {
        String s = Integer.toBinaryString(N);
        int sum = 0;
        //  101    010
        for (char c : s.toCharArray()) {    
            sum <<= 1;        
            if (c == '0')                
                sum += sum + 1;
            /*
            else 
                sum = sum << 1 + 1;
            */
        }
        return sum;
    }
}
```

运行

```
输入：
10
输出：
9
预期：
5
```



计算主要就是移位和加上当前位上的值

而 0 是不需要另外加的.

所以遇到 "1" 的时候是可以不用考虑的.

而且, 这道题只要会做正常的移位运算后, 反码也是一样的.

所以, 经过仔细查看后, 以 10010 为例(原码)

> 10010
>
> 1
>
> 10
>
> 1001
>
> 10010

图示

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-12-10-%E6%95%B0%E5%AD%A6-1009-%E5%8D%81%E8%BF%9B%E5%88%B6%E6%95%B4%E6%95%B0%E7%9A%84%E5%8F%8D%E7%A0%81/draft.PNG" width="60%">

每一步都会移位, 每一步都会加上当前位数. 而 0 可以忽略不加.

于是, 这一次就拿 把移位调上前面去了

```java
class Solution {
    public int bitwiseComplement(int N) {
        String s = Integer.toBinaryString(N);
        int sum = 0;
        //  101    010
        for (char c : s.toCharArray()) {    
            sum <<= 1;        
            if (c == '0')                
                sum += 1;                             
        }
        return sum;
    }
}
```

运行通过了

```
执行用时：1 ms, 在所有 Java 提交中击败了28.43%的用户
```



继调试后, 终于出结果了.



#### 本期leetcode	

还是学到上一道题中运用移位运算符的方法.



