#### Question [剑指 Offer 13. 机器人的运动范围](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)

tag##



#### Description



#### Analysis





#### Code

> 截止22点24分, 考虑了前两种情况, ①单行or单列; ②行列为 10 以内的情况.

```java
class Solution {
    public int movingCount(int m, int n, int k) {
        int middle = (m-1) + (n-1);    //  k 的重要的参数对照, 因为它是在 m,n 个位内横纵坐标数位和的最大值
        int result = 0;
        //  宫格的行或列其中一个为 1 的 3 种情况:
        if (m == 1 || n == 1) {
            if (k == 0)
                result = 1;
            else if (0 < k && k < m*n)
                result = k+1;
            else    
                result = m*n;
        }
        //  宫格的行和列都小于 10: 原数字计算数位和的 3 种情况:
        if ((1 < m && m <= 10 ) && (1 < n && n <= 10)) {
            // i. k = 0 时, 总有(0,0)
            if (k == 0)
                result = 1;
            //  ii. k 位于 0 和 middle 之间时, 减去右下角的方格
            //  根据矩阵横纵坐标和沿正对角线对称的排列, 右下角不满足的坐标个数总是起点为 1, 终点为 delta 的累加和
            else if (0 < k && k < middle) {
                int delta = k - middle;         //  delta 为 middle 与 k 的差值
                int sub = 0;
                for (int i=1; i<=delta; i++) {   //  计算右下角不满足的方格个数
                    sub += i;
                }
                result = middle - sub;          //  用总方格数减去右下角的方格个数
            }
            //  iii. k >= middle 时, 宫格中方格都可以走. 即 m*n 个.
             else if (k >= middle)   
                result = m*n;
        }
        return result;
    }
}
```

目前的执行结果:

```
10 / 49 个通过测试用例
状态：解答错误
提交时间：6 分钟前
输入：
16
8
4
输出：
0
预期：
15
```





