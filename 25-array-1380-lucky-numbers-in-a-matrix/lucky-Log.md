#### Question [矩阵中的幸运数](https://leetcode-cn.com/problems/lucky-numbers-in-a-matrix/)/[Lucky Numbers in a Matrix](https://leetcode-cn.com/problems/lucky-numbers-in-a-matrix/)

tag#array# #two-dimensional array#



#### Description

```
给你一个 m * n 的矩阵，矩阵中的数字 各不相同 。请你按 任意 顺序返回矩阵中的所有幸运数。

幸运数是指矩阵中满足同时下列两个条件的元素：

在同一行的所有元素中最小
在同一列的所有元素中最大
 

示例 1：

输入：matrix = [[3,7,8],[9,11,13],[15,16,17]]
输出：[15]
解释：15 是唯一的幸运数，因为它是其所在行中的最小值，也是所在列中的最大值。
示例 2：

输入：matrix = [[1,10,4,2],[9,3,8,7],[15,16,17,12]]
输出：[12]
解释：12 是唯一的幸运数，因为它是其所在行中的最小值，也是所在列中的最大值。
示例 3：

输入：matrix = [[7,8],[1,2]]
输出：[7]
 

提示：

m == mat.length
n == mat[i].length
1 <= n, m <= 50
1 <= matrix[i][j] <= 10^5
矩阵中的所有元素都是不同的

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/lucky-numbers-in-a-matrix
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```





#### Analysis

题目分析

有题可得, 如果一个数(矩阵中)既是行中最小, 又是列中最大, 那么它就是一个幸运数.

而给出的方法返回值类型是 `List<Integer>` 说明一个矩阵中有可能存在多个这样的幸运数.



思路分析

根据 *显示提示1* 中的提示

> Find out and save the minimum of each row and maximum of each column in two lists.
>
> 找到每一行的最小值和每一列的最大值.

各拿一个数组收录行最小 `rowMin` 和列最大 `colMax`

而题目中又交代了矩阵中每一个数字各不相同, 这就说明了可以通过两个数组的值比较确定是同一个坐标值. 而不用考虑值相等而又可能属于不同位置上的数了.



#### Code

##### commit 1

```java
class Solution {
    public List<Integer> luckyNumbers (int[][] matrix) {
            int m = matrix[0].length;
            int n = matrix.length;
            int[] rowMin = new int[m];  //  记录行中最小
            int[] colMax = new int[n];  //  记录列中最大
            int rpc = 0;
            int cpc = 0;
            List<Integer> list = new ArrayList<Integer>();
            //  行最小
            for (int x = 0; x < n; x++) {    //  matrix x,y 纵坐标待定 等当前行遍历结束后纵坐标自增
                int min = matrix[x][0]; 
                for (int y = 0; y < m; y++) {       //  遍历当前行数组
                    if (matrix[x][y] < min) {
                        min = matrix[x][y];                    
                    }
                }                
                rowMin[rpc] = min;
                rpc++;
                //   查找完当前行最小后更新容器数组索引
            }
            //  列最大
            for (int y = 0; y < n; y++)  {   //  matrix  x,y 横坐标待定 等当前列遍历结束后横坐标自增
                
                int max = matrix[0][y];
                for (int x = 0; x < n; x++) {                    
                    if (matrix[x][y] > max) {
                        max = matrix[x][y];
                    }
                }
                colMax[cpc] = max;
                cpc++;
                //  查抄完当前列最大更新容器数组索引
            }
            for (int c = 0; c < n; c++) {       
                for (int r = 0; r < m; r++) {   //  列不动行动, 当有重合的项出现时收录其中任意一个
                    if (rowMin[r] == colMax[c]) {
                        list.add(colMax[r]);
                    }
                }
            }
            return list;
    }
}
```

执行结果:

```
输入：
[[3,7,8],[9,11,13],[15,16,17]]
输出：
[17]
预期结果：
[15]
```



##### 评论区优秀答案

```java
class Solution {
    public List<Integer> luckyNumbers (int[][] matrix) {
        int row = matrix.length;
        int col = matrix[0].length;
        int[] rows = new int[row];
        int[] cols = new int[col];
        Arrays.fill(rows, Integer.MAX_VALUE);
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                int cur = matrix[i][j];
                rows[i] = Math.min(cur, rows[i]);
                cols[j] = Math.max(cur, cols[j]);
            }
        }
        List<Integer> res = new ArrayList<>();
        for (int i = 0; i < row; i++) {
            for (int j = 0; j < col; j++) {
                int cur = matrix[i][j];
                if (cur == rows[i] && cur == cols[j]) {
                    res.add(cur);
                }
            }
        }
        return res;
    }
}
```









 
