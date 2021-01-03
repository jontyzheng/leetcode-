#### Question [970. 强整数](https://leetcode-cn.com/problems/powerful-integers/)

tag##



#### Description

```
给定两个正整数 x 和 y，如果某一整数等于 x^i + y^j，其中整数 i >= 0 且 j >= 0，那么我们认为该整数是一个强整数。

返回值小于或等于 bound 的所有强整数组成的列表。

你可以按任何顺序返回答案。在你的回答中，每个值最多出现一次。

 

示例 1：

输入：x = 2, y = 3, bound = 10
输出：[2,3,4,5,7,9,10]
解释： 
2 = 2^0 + 3^0
3 = 2^1 + 3^0
4 = 2^0 + 3^1
5 = 2^1 + 3^1
7 = 2^2 + 3^1
9 = 2^3 + 3^0
10 = 2^0 + 3^2
示例 2：

输入：x = 3, y = 5, bound = 15
输出：[2,4,6,8,10,14]
 

提示：

1 <= x <= 100
1 <= y <= 100
0 <= bound <= 10^6

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/powerful-integers
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```







#### Code

```java
class Solution {
    
    public List<Integer> powerfulIntegers(int x, int y, int bound) {
        
        //  集合申请
        Set<Integer> set = new HashSet<>(); 
        /*
        任何数的 0 次方都为 1, 从 1 开始        
        */
        /*
        a: x 的 i 次方
        b: y 的 j 次方

        x 的 i 次方
        */
        for (int a = 1; a < bound; a = a * x) {
            for (int b = 1; a + b <= bound; b = b * y) {
                set.add(a + b);
                if (y == 1)
                    break;
            }
            if (x == 1)
                break;
        }
        return new ArrayList<>(set);
    }
}
```







#### 分析

###### 强整数

所谓强整数, 就是 x <sup>i</sup> 和 y <sup>j</sup> 的和. 

其中,  x 和 y 是给出的. 和也是限定的.

即不超出指定范围的情况下求出所有 x 和 y 次方的组合. (其中 i 和 j 可以为 0 或者任何数)

以  2, 3 为例,  

当 i 和 j 为 0 时, 它们的幂总是 1, 所以 2 总是满足条件.

之后, sum 等于其中一个乘以本身, 因为 x <sup>0</sup> 总是为 1, 所以 x <sup>i</sup> 的变化可以依次表示为 1, 1* x, x * x, x  * x * x,... 在原来基础上累乘的形式.

同理, y <sup>j</sup> 也可以表示成相同的递乘形式.



但是由于要统计到 i 和 j 所有可能的情况, 这时候就是统计依次 former * x 或 former * y 的次数了.

用嵌套的 for 循环可以遍历到所有可能的情况.



假设用 a 表示 x * x *..., b 表示 y * y *...(后面不断更新 ab)

条件: a + b <= bound, 不会大于求和的范围.



控制循环:

-











#### 测试用例过滤







#### 讲讲你一开始的想法

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2021-01-03-%E6%95%B0%E5%AD%A6-970-%E5%BC%BA%E6%95%B4%E6%95%B0/QQ%E5%9B%BE%E7%89%8720210103221808.jpg" width="50%">

一开始想的就是知道它是怎么回事, 但是看到 i 和 j 都要异步变化的时候就不知道怎么做了.











#### 本期leetcode	

强整数的求解过程.



