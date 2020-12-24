#### Question [812. 最大三角形面积](https://leetcode-cn.com/problems/largest-triangle-area/)

tag##



#### Description

```
给定包含多个点的集合，从其中取三个点组成三角形，返回能组成的最大三角形的面积。

示例:
输入: points = [[0,0],[0,1],[1,0],[0,2],[2,0]]
输出: 2
解释: 
这五个点如下图所示。组成的橙色三角形是最大的，面积为2。
```

<img src="" zoom="50%">



```
注意:

3 <= points.length <= 50.
不存在重复的点。
 -50 <= points[i][j] <= 50.
结果误差值在 10^-6 以内都认为是正确答案。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/largest-triangle-area
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```









#### Code

```java
class Solution {
    // 执行用时：15 ms 必须遍历所有可能的两个点
    public double largestTriangleArea(int[][] points) {
        float area = 0;
        float max= 0;
        int n =points.length;
        for(int i =0;i<n;i++)
            for(int j = 0;j<n;j++)
                for(int k = 0;k<n;k++)
                {
                    if(i!=j&&i!=k&&j!=k)
                    {
                        // S=(x1y2+x2y3+x3y1-x1y3-x2y1-x3y2) /2;
                        area = ((float)points[i][0]*(float)points[j][1]+
                                (float)points[j][0]*(float)points[k][1]+
                                (float)points[k][0]*(float)points[i][1] - 
                                (float)points[i][0]*(float)points[k][1]-
                                (float)points[j][0]*(float)points[i][1]-
                                (float)points[k][0]*(float)points[j][1]);
                        area/=2.0f;
                        if(area>max) max= area;
                    }
                }
        return max;
    }
}
```







#### 分析

-





#### 测试用例过滤

-





#### 讲讲你一开始的想法

-







#### 本期 leetcode	





