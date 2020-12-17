#### Question [1232. 缀点成线](https://leetcode-cn.com/problems/check-if-it-is-a-straight-line/)

tag##



#### Description

```
在一个 XY 坐标系中有一些点，我们用数组 coordinates 来分别记录它们的坐标，其中 coordinates[i] = [x, y] 表示横坐标为 x、纵坐标为 y 的点。

请你来判断，这些点是否在该坐标系中属于同一条直线上，是则返回 true，否则请返回 false。

 

示例 1：

```

<img src="" width="50%">



```
输入：coordinates = [[1,2],[2,3],[3,4],[4,5],[5,6],[6,7]]
输出：true
示例 2：

```

<img src="" width="50%">

```
输入：coordinates = [[1,1],[2,2],[3,4],[4,5],[5,6],[7,7]]
输出：false
 

提示：

2 <= coordinates.length <= 1000
coordinates[i].length == 2
-10^4 <= coordinates[i][0], coordinates[i][1] <= 10^4
coordinates 中不含重复的点

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/check-if-it-is-a-straight-line
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```









#### Code

```java
class Solution {
    //执行用时：1 ms
    public boolean checkStraightLine(int[][] coordinates) {
        boolean isStraightLine = true;
        int rows = coordinates.length;

        double deltaY0 = coordinates[1][1] - coordinates[0][1];
        double deltaX0 = coordinates[1][0] - coordinates[0][0];
        
        if (rows == 2)
            return true;
        
        if (deltaX0 == 0) {                 //  update: 分垂直线斜率不存在的情况
            for (int i = 2; i < rows; i++) {
                double delX = coordinates[i][0] - coordinates[0][0];
                if (delX != 0) {
                    return false;
                }
            }
        }
        else {
            double k = deltaY0/deltaX0;
            for (int i = 2; i < rows; i++) {
                double delY = coordinates[i][1] - coordinates[0][1];
                double delX = coordinates[i][0] - coordinates[0][0];                
                double slope = delY / delX;
                if (slope != k) {
                    isStraightLine = false;
                    break;
                }
            }
        }
        return isStraightLine;
    }
}
```







#### 分析

现有一组坐标, 要求判断它们在同一条直线上.

基本思路是求斜率, 如果有偏移的点就可以知道这一组点不位于同一条直线上.

> 斜率公式:
>
> k = (y1 - y0) / (x1 = x0)



分别计算前后两点(或者每一点与第一点之间的斜率), 以第一个点和第二点之间的斜率为基准. 每次求出后面的点和第一个点之间的斜率.

若遇到不一致的点说明偏移直线, 可判断为该组坐标不在同一条直线上.



因为除法的结果要用作数值比较, 所以除法的结果应该用 double 接收.





#### 测试用例过滤

##### I.整数的除法取整

```java
class Solution {
    public boolean checkStraightLine(int[][] coordinates) {
        int rows = coordinates.length;
        int k = 0;
        
        k = (coordinates[1][1] - coordinates[0][1]) / (coordinates[1][0] - coordinates[0][0]);

        boolean isStraightLine = true;
        
        if (rows == 2)
            return true;

        outer:
        for (int i = 2; i < rows; i++) {
            for (int j = 0; j < 2; j++) {
                int deltaY = coordinates[i][1] - coordinates[0][1];
                int deltaX = coordinates[i][0] - coordinates[0][0];
                int slope = deltaY / deltaX;
                if (slope != k) {
                    isStraightLine = false;
                    break outer;
                }
            }
        }
        return isStraightLine;
    }
}
```



```
输入：[[1,1],[2,2],[3,4],[4,5],[5,6],[7,7]]
输出：true
预期：false
```

> 解释:
>
> k<sub>0</sub> 为 1, (4-2)/(3/1) = 1 (1.5 被截取) 导致相等, 没有判断出来. 所以造成会返回 true.

###### 方法: 修改斜率的计算公式

修改 deltaY 和 deltaX 的接收类型, 浮点数之间的运算可以得到除法额的完整小数.





##### II.分母为零的规则

```java
class Solution {
    public boolean checkStraightLine(int[][] coordinates) {
        int rows = coordinates.length;
        double k = 0.0;
        
        k = (coordinates[1][1] - coordinates[0][1]) / (coordinates[1][0] - coordinates[0][0]);

        boolean isStraightLine = true;
        
        if (rows == 2)
            return true;
        
        for (int i = 2; i < rows; i++) {    //  update: 删除内循环因子 j, 循环体中并没有用到        
            double deltaY = coordinates[i][1] - coordinates[0][1];  
            //  update: 修改 deltaY 的 int 为 double 
            double deltaX = coordinates[i][0] - coordinates[0][0];
            double slope = deltaY / deltaX; //  update: 修改 int 为 double
            if (slope != k) {
                isStraightLine = false;
                break;
            }            
        }
        return isStraightLine;
    }
}
```



```
执行出错信息：
Line 6: java.lang.ArithmeticException: / by zero
最后执行的输入：
[[0,0],[0,1],[0,-1]]
```

> 解释:
>
> 当整数除以 0 的时候会抛出数学异常.
>
> (1-0) / (0 - 0)

###### 方法: 分情况讨论

已知两点坐标求斜率没有别的方法, 所以分情况讨论.

直线垂直于 y 轴属于直线斜率不存在的情况.

分情况讨论:

①. 当 k 不存在的时候, 最开始两点位于同一条垂线上, 横坐标之差为 0, 这时候依次比较后面的点与第一个点的**横坐标之差**是否为 0. 

如果位于后面的点的横坐标与第一个点的横坐标之差为 0, 说明总是在同一条垂线上. 若有偏移则返回 false;

②. 当 k 不存在, 按照前面的方法比较**斜率**.







III

```java
class Solution {
    //49/79
    public boolean checkStraightLine(int[][] coordinates) {
        boolean isStraightLine = true;
        int rows = coordinates.length;

        int deltaY0 = coordinates[1][1] - coordinates[0][1];
        int deltaX0 = coordinates[1][0] = coordinates[0][0];
        
        if (rows == 2)
            return true;
        
        if (deltaX0 == 0) {				//  update: 分垂直线斜率不存在的情况
            for (int i = 2; i < rows; i++) {
                int delX = coordinates[i][0] - coordinates[0][0];
                if (delX != 0) {
                    return false;
                }
            }
        }
        else {
            int k = deltaY0/deltaX0;
            for (int i = 2; i < rows; i++) {
                double delX = coordinates[i][0] - coordinates[0][0];
                double delY = coordinates[i][1] - coordinates[0][1];
                double slope = delY / delX;
                if (slope != k) {
                    isStraightLine = false;
                    break;
                }
            }
        }
        return isStraightLine;
    }
}
```



```
输入：[[2,1],[4,2],[6,3]]
输出：false
预期结果：true
```

> 解释:
>
> 基础斜率 k: 出现过的问题.
>
> 公式用的都是 int, 除法截取.

###### 方法: 将涉及到斜率计算的变量设为 double 类型





###### V.非代码逻辑问题

```java
class Solution {
    public boolean checkStraightLine(int[][] coordinates) {
        boolean isStraightLine = true;
        int rows = coordinates.length;

        double deltaY0 = coordinates[1][1] - coordinates[0][1];
        double deltaX0 = coordinates[1][0] = coordinates[0][0];
        
        if (rows == 2)
            return true;
        
        if (deltaX0 == 0) {                 //  update: 分垂直线斜率不存在的情况
            for (int i = 2; i < rows; i++) {
                double delX = coordinates[i][0] - coordinates[0][0];
                if (delX != 0) {
                    return false;
                }
            }
        }
        else {
            double k = deltaY0/deltaX0;		//	update: 将斜率运算的变量类型设置为浮点类型
            for (int i = 2; i < rows; i++) {
                double delY = coordinates[i][1] - coordinates[0][1];
                double delX = coordinates[i][0] - coordinates[0][0];                
                double slope = delY / delX;
                if (slope != k) {
                    isStraightLine = false;
                    break;
                }
            }
        }
        return isStraightLine;
    }
}
```



```
输入：[[2,4],[2,5],[2,8]]
输出：false
预期：true
```

> 解释:
>
> 同在垂直线上的一排
>
> 第四行代码出现手误

###### 方法: 检查代码

`double deltaX0 = coordinates[1][0] = coordinates[0][0];`



##### VI. 修改

```java
class Solution {
    //执行用时：1 ms
    public boolean checkStraightLine(int[][] coordinates) {
        boolean isStraightLine = true;
        int rows = coordinates.length;

        double deltaY0 = coordinates[1][1] - coordinates[0][1];
        double deltaX0 = coordinates[1][0] - coordinates[0][0];
        
        if (rows == 2)
            return true;
        
        if (deltaX0 == 0) {                 //  update: 分垂直线斜率不存在的情况
            for (int i = 2; i < rows; i++) {
                double delX = coordinates[i][0] - coordinates[0][0];
                if (delX != 0) {
                    return false;
                }
            }
        }
        else {
            double k = deltaY0/deltaX0;
            for (int i = 2; i < rows; i++) {
                double delY = coordinates[i][1] - coordinates[0][1];
                double delX = coordinates[i][0] - coordinates[0][0];                
                double slope = delY / delX;
                if (slope != k) {
                    isStraightLine = false;
                    break;
                }
            }
        }
        return isStraightLine;
    }
}
```



```
执行用时：1 ms, 在所有 Java 提交中击败了10.19%的用户
```







#### 讲讲你一开始的想法

一开始就想到了直线斜率.

在实际运算的过程发现原来我没有考虑到"整数除法截取", 也没有考虑到"斜率不存在"的情况.

哇真的是.





#### 本期leetcode	

两点之间求斜率, 涉及到除法结果的相互匹配, 使用浮点类型.

程序中使用斜率也要考虑直线斜率不存在的情况.



