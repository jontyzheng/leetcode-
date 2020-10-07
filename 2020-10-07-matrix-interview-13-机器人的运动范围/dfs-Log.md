#### Question [剑指 Offer 13. 机器人的运动范围](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)

tag#剑指 offer# #matrix# #DFS#



#### Description

```
地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

 

示例 1：

输入：m = 2, n = 3, k = 1
输出：3
示例 2：

输入：m = 3, n = 1, k = 0
输出：1
提示：

1 <= n,m <= 100
0 <= k <= 20
```



#### Analysis

一开始发现的只有对称规律, 然后也知道怎么计算两位数的数位和, 便采用分情况计数格子的方法.

后来才知道, 当两位的数时候并不是那么对称.



#### Code

```java
class Solution {
    public int movingCount(int m, int n, int k) {
        // 评论区答案: 
        // 执行用时：1 ms, 在所有 Java 提交中击败了85.05%的用户
        boolean[][] visited = new boolean[m][n];
        return dfs(0, 0, m, n, k, visited);
    }

    private int dfs(int i, int j, int m, int n, int k, boolean visited[][]) {
        if (i < 0 || i >= m || j < 0 || j >= n || (i/10 + i%10 + j/10 + j%10) > k || visited[i][j]) {
            return 0;
        }
        visited[i][j] = true;
        return dfs(i + 1, j, m, n, k, visited) + dfs(i - 1, j, m, n, k, visited) + 
               dfs(i, j + 1, m, n, k, visited) + dfs(i, j - 1, m, n, k, visited) + 1;
    }
}
```



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
        //  宫格的行和列都小于 10: 常规计算数位和的 3 种情况:
        if ((1 < m && m < 10 ) && (1 < n && n < 10)) {
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
        // 宫格的行和列为两位数, 需要/10和%10计算数位和: 略
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



