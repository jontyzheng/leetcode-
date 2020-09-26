#### Question [二维数组中的查找](https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

tag#剑指 offer# #array#



#### Description

```
在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

 

示例:

现有矩阵 matrix 如下：

[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
给定 target = 5，返回 true。

给定 target = 20，返回 false。

 

限制：

0 <= n <= 1000

0 <= m <= 1000
```



#### Analysis

给定一个行列都是"递增"顺序的二维数组中看能不能找到给定的一个数字.

条件循环, 因为每一行都是从小到大递增的, 所以只有指定数字落在行最左和最右中间才有可能在那一行找到指定数字. 

> 限制: m, n 都有可能为 0, 排除掉行/rows 为 0 的情况, 并且, 当列为 0 的时候, 不存在列/cols.



#### Code

```java
class Solution {
    public boolean findNumberIn2DArray(int[][] matrix, int target) {
        int rows = matrix.length;        
        int cols = 0;
        // rows == 0
        if (rows == 0) {
            return false;
        }
        
        if (matrix[0].length > 0) {
            cols = matrix[0].length;
        } 
        // cols == 0
        else
            return false;
        // row == col == 1            
        if (rows == 1 && cols == 1)
            return matrix[0][0] == target;
        int line = -1;
        boolean found = false;
        
        for (int i = 0; i < rows; i++) {
            if (target >= matrix[i][0] && target <= matrix[i][cols-1]) { // [[1,1]] 1 true 非递增
                for (int j = 0; j < cols; j++) {
                    if (target == matrix[i][j]) {
                        found = true;
                        break;
                    }
                }                
            }
        }        
        return found;
    }
}
```

运行效果:

执行结果：

通过

显示详情

执行用时：1 ms, 在所有 Java 提交中击败了16.06%的用户



> 之所以在递增打引号, 是因为碰到了一个 [][][[1, 1]] 的测试用例. 所以在条件循环的条件里头加上了等号.





