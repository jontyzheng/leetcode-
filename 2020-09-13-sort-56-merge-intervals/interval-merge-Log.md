#### Question 区间合并/[56. Merge Intervals](https://leetcode-cn.com/problems/merge-intervals/)

tag#sort#



#### Description

```
给出一个区间的集合，请合并所有重叠的区间。

 

示例 1:

输入: intervals = [[1,3],[2,6],[8,10],[15,18]]
输出: [[1,6],[8,10],[15,18]]
解释: 区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6].
示例 2:

输入: intervals = [[1,4],[4,5]]
输出: [[1,5]]
解释: 区间 [1,4] 和 [4,5] 可被视为重叠区间。
注意：输入类型已于2019年4月15日更改。 请重置默认代码定义以获取新方法签名。

 

提示：

intervals[i][0] <= intervals[i][1]

```



#### Analysis

见 commit 1 中注释.





#### Code

答案:

```java
class Solution {
    public int[][] merge(int[][] arr) {
        if(arr == null || arr.length<=1)
            return arr;
        List<int[]> list = new ArrayList<>();
        //Arrays.sort(arr,(a,b)->a[0]-b[0]);
        Arrays.sort(arr,new Comparator<int[]>(){
            @Override
            public int compare(int[] a,int[] b){
                return a[0]-b[0];
            }
        });
        int i=0;
        int n = arr.length;
        while(i<n){
            int left = arr[i][0];
            int right = arr[i][1];
            while(i<n-1 && right>=arr[i+1][0]){
                right = Math.max(right,arr[i+1][1]);
                i++;
            }
            list.add(new int[] {left,right});
            i++;
        }
        return list.toArray(new int[list.size()][2]);
    }
}
```



##### commit 1

> 先统计需要消元的个数, 拿到需要申请的列数 `count` , 然后再申请新的二维数组进行赋值.
>
> 结果超出时间限制.
>
> 要是知道可以伸缩自如的数据结构用来直接对目标区间的两个端点值进行保存, 就可以省略掉统计的 `for` 了, 最后那个得到新区间的数据结构再变数组返回,

原答案:

```java
class Solution {
    public int[][] merge(int[][] intervals) {
        //  相邻的两个区间, 右端点和左端点有交叉即满足合并条件 右端点 > 左端点, 组成新的区间, 更新数组
        int row = intervals.length;  //  列
        //  默认的就是两列, 一个二元组.
        int column = intervals[0].length;   //  行
        int count = 0;                      //   count 将作为新数组申请行的依据
        for (int i = 0; i < row-1; i++) {   //  由于方法体内用到的是 i+1
            int j = i+1;
            //  那当前的右端点和下一个的左端点继续比较
            if (intervals[i][1] > intervals[j][0]) {
                count++;    //  记录需要消掉的个数.
                i--;        //  回到更新的当前坐标, 重新与比对
                j = j+1;    //  更新下一个需要比对的坐标
                //  临时保留二元组
            }
        }
        int[][] newArr = new int[count][2];
        for (int i = 0; i < row; i++) {
            //  右端点>(下一个的)右端点, 比右端点更大的左端点的左端点一定比原来的左端点更大
            int j = i + 1;
            if (intervals[i][1] > intervals[j][0]) {
                newArr[i][0] = intervals[i][0];
                newArr[i][1] = intervals[j][1];
                i--;
                j++;    //  跳过被合并的坐标
            }
        }
        return newArr;
    }
}
```



commit 2

commit 3





