

#### Question: [重塑矩阵](https://leetcode-cn.com/problems/reshape-the-matrix/)/[Reshape the Matrix](https://leetcode-cn.com/problems/reshape-the-matrix/)

tag#array#

#### Description

```
在MATLAB中，有一个非常有用的函数 reshape，它可以将一个矩阵重塑为另一个大小不同的新矩阵，但保留其原始数据。

给出一个由二维数组表示的矩阵，以及两个正整数r和c，分别表示想要的重构的矩阵的行数和列数。

重构后的矩阵需要将原始矩阵的所有元素以相同的行遍历顺序填充。

如果具有给定参数的reshape操作是可行且合理的，则输出新的重塑矩阵；否则，输出原始矩阵。

示例 1:

输入: 
nums = 
[[1,2],
 [3,4]]
r = 1, c = 4
输出: 
[[1,2,3,4]]
解释:
行遍历nums的结果是 [1,2,3,4]。新的矩阵是 1 * 4 矩阵, 用之前的元素值一行一行填充新矩阵。
示例 2:

输入: 
nums = 
[[1,2],
 [3,4]]
r = 2, c = 4
输出: 
[[1,2],
 [3,4]]
解释:
没有办法将 2 * 2 矩阵转化为 2 * 4 矩阵。 所以输出原矩阵。
注意：

给定矩阵的宽和高范围在 [1, 100]。
给定的 r 和 c 都是正数。
```



#### Analysis

想法很简单, 将原来的二维变一维, 再拿一维按照给到的行和列依次赋值.

要注意的是的几点:

1. 二维数组的行列计算:

   行: nums[0].length

   列: nums.length

2. 二维数组的从第一个元素依次排列的顺序.

   (0,0), (0,1), (0,2)

   (1,0), (1,1), (1,2), 

   (2,0), (2,1), (2,2)

   第一行当列标达到终点的时候, 行标开始加 1, 列标归零. 以此类推, 每行都是这样.



##### commit 1

```java
class Solution {
    public int[][] matrixReshape(int[][] nums, int r, int c) {
        //  给定的 r 和 c 都是正数: 不用验参了        
        int numCount = nums[0].length*nums.length;
        if (r*c != numCount)
            return nums;
        int[] tempArr = new int[numCount];     
        //  旧数组的迁移
        for (int i = 0,j = 0,z = 0; z < numCount; z++, j++) {   
            tempArr[z] = nums[i][j];
            /*
            java.lang.ArrayIndexOutOfBoundsException: Index 2 out of bounds for length 2             */
            if (j == nums[0].length - 1) {       // 修改: 落在行的最后一位时列标归零, 行标自增
                i++;
                j = 0;                      
            }            
        }
        //  新数组的重建
        int[][] newArr = new int[r][c];
        int k = 0;
        int y = 0;
        for(int i = 0; i < numCount; i++) {      //  修改: 条件是列, 当行标达到顶时更新列标, 行标归零   
            if (y <= c-1) {
                newArr[k][y] = tempArr[i];
                y++;   
                k = 0;                 
            }
            else 
                k++;           
        }
        return newArr;
    }
}
```

> 数组越界现象



#### 答案

```java

```



