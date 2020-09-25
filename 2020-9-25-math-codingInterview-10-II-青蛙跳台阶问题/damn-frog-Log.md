#### Question 青蛙跳台阶问题

tag#剑指 offer# #math#



#### Description

```
一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 n 级的台阶总共有多少种跳法。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

示例 1：

输入：n = 2
输出：2
示例 2：

输入：n = 7
输出：21
示例 3：

输入：n = 0
输出：1
提示：

0 <= n <= 100

```

注意：本题与主站 70 题相同：https://leetcode-cn.com/problems/climbing-stairs/

#### Analysis

遍历情况多, 如果只跳一次 2 步还好, 可以当作将 2 插入到其它 1 的空位中间, 得到的每一种顺序都是一种其中一种情况. C<sub>(x+1)</sub><sup>1</sup> , (x 为 1 的个数.) 要是多了许多 2 就不知道怎么搞了.



#### Code

来自评论区大佬

```java
class Solution {
    // 执行用时 :0 ms, 在所有 Java 提交中击败了100.00%的用户内存消耗 :
    // 33.2 MB, 在所有 Java 提交中击败了70.25%的用户
    public int climbStairs(int n) {
        if(n<=2){
            return n;
        }
        int i1 = 1;
        int i2 = 2;
        for(int i=3;i<=n;i++){
            int temp = i1+i2;
            i1 = i2;
            i2 = temp;
        }
        return i2;
    }
}
```







