#### Question [子矩形查询](https://leetcode-cn.com/problems/subrectangle-queries/)

tag#array#



#### Description

```
请你实现一个类 SubrectangleQueries ，它的构造函数的参数是一个 rows x cols 的矩形（这里用整数矩阵表示），并支持以下两种操作：

1. updateSubrectangle(int row1, int col1, int row2, int col2, int newValue)

用 newValue 更新以 (row1,col1) 为左上角且以 (row2,col2) 为右下角的子矩形。
2. getValue(int row, int col)

返回矩形中坐标 (row,col) 的当前值。
 

示例 1：

输入：
["SubrectangleQueries","getValue","updateSubrectangle","getValue","getValue","updateSubrectangle","getValue","getValue"]
[[[[1,2,1],[4,3,4],[3,2,1],[1,1,1]]],[0,2],[0,0,3,2,5],[0,2],[3,1],[3,0,3,2,10],[3,1],[0,2]]
输出：
[null,1,null,5,5,null,10,5]
解释：
SubrectangleQueries subrectangleQueries = new SubrectangleQueries([[1,2,1],[4,3,4],[3,2,1],[1,1,1]]);  
// 初始的 (4x3) 矩形如下：
// 1 2 1
// 4 3 4
// 3 2 1
// 1 1 1
subrectangleQueries.getValue(0, 2); // 返回 1
subrectangleQueries.updateSubrectangle(0, 0, 3, 2, 5);
// 此次更新后矩形变为：
// 5 5 5
// 5 5 5
// 5 5 5
// 5 5 5 
subrectangleQueries.getValue(0, 2); // 返回 5
subrectangleQueries.getValue(3, 1); // 返回 5
subrectangleQueries.updateSubrectangle(3, 0, 3, 2, 10);
// 此次更新后矩形变为：
// 5   5   5
// 5   5   5
// 5   5   5
// 10  10  10 
subrectangleQueries.getValue(3, 1); // 返回 10
subrectangleQueries.getValue(0, 2); // 返回 5
示例 2：

输入：
["SubrectangleQueries","getValue","updateSubrectangle","getValue","getValue","updateSubrectangle","getValue"]
[[[[1,1,1],[2,2,2],[3,3,3]]],[0,0],[0,0,2,2,100],[0,0],[2,2],[1,1,2,2,20],[2,2]]
输出：
[null,1,null,100,100,null,20]
解释：
SubrectangleQueries subrectangleQueries = new SubrectangleQueries([[1,1,1],[2,2,2],[3,3,3]]);
subrectangleQueries.getValue(0, 0); // 返回 1
subrectangleQueries.updateSubrectangle(0, 0, 2, 2, 100);
subrectangleQueries.getValue(0, 0); // 返回 100
subrectangleQueries.getValue(2, 2); // 返回 100
subrectangleQueries.updateSubrectangle(1, 1, 2, 2, 20);
subrectangleQueries.getValue(2, 2); // 返回 20
 

提示：

最多有 500 次updateSubrectangle 和 getValue 操作。
1 <= rows, cols <= 100
rows == rectangle.length
cols == rectangle[i].length
0 <= row1 <= row2 < rows
0 <= col1 <= col2 < cols
1 <= newValue, rectangle[i][j] <= 10^9
0 <= row < rows
0 <= col < cols
```





#### Analysis

由题可知, 需要写的就是一个实现一个类, 具体只需实现其中的三个方法:

1. 构造方法: 给内置的二维数组赋值;
2. 更新矩阵方法: 根据提供的上下界, 将另一个 `newValue` 替换掉原矩阵中的值;
3. 获取矩阵中的值: 根据提供的坐标, 返回矩阵中对应位置上的数值.

题目中输入的演示, 是程序外部方法调用的顺序, 假设程序会按照第一行输入的顺序执行, 我们只需要实现被调用的方法体就可以了.

其中, 因为每个方法都要对同一个数组进行操作 (无论是赋值, 修改, 还是返回), 所以把它设置成一个类的内置属性成员 (全局变量), 构造方法就负责将形参的二维数组指向给内置数组即可.



图示:

![](https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-9-22-array-1476-subrectangle-queries/matrix.PNG)

#### Code

```java
class SubrectangleQueries {
    //  构造方法 rectangle[0].length*recrangle.length
    int[][] matrix = null;
    public SubrectangleQueries(int[][] rectangle) {
        this.matrix =  rectangle;
    }
    
    public void updateSubrectangle(int row1, int col1, int row2, int col2, int newValue) {
        for (int i = row1; i <= row2; i++) {
            for (int j = col1; j <= col2; j++) {
                matrix[i][j] = newValue;
            }
        }
    }
    
    public int getValue(int row, int col) {
        //  数据来源
        return matrix == null? -1:matrix[row][col];
    }
}

/**
 * Your SubrectangleQueries object will be instantiated and called as such:
 * SubrectangleQueries obj = new SubrectangleQueries(rectangle);
 * obj.updateSubrectangle(row1,col1,row2,col2,newValue);
 * int param_2 = obj.getValue(row,col);
 */
```

执行效果:

执行用时：31 ms, 在所有 Java 提交中击败了78.02%的用户



感觉这一道 medium 的不难.

只需将原矩阵按照给定的上下界用新值替换就可以了. 就是形式不一样, 这次是实现一个类.





