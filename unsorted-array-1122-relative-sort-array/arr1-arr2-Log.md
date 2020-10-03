#### Question title: [数组的相对排序](https://leetcode-cn.com/problems/relative-sort-array/)/[Relative Sort Array](https://leetcode-cn.com/problems/relative-sort-array/)

tag#array#



#### Description

```
给你两个数组，arr1 和 arr2，

arr2 中的元素各不相同
arr2 中的每个元素都出现在 arr1 中
对 arr1 中的元素进行排序，使 arr1 中项的相对顺序和 arr2 中的相对顺序相同。未在 arr2 中出现过的元素需要按照升序放在 arr1 的末尾。

 

示例：

输入：arr1 = [2,3,1,3,2,4,6,7,9,2,19], arr2 = [2,1,4,3,9,6]
输出：[2,2,2,1,4,3,3,9,6,7,19]
 

提示：

arr1.length, arr2.length <= 1000
0 <= arr1[i], arr2[i] <= 1000
arr2 中的元素 arr2[i] 各不相同
arr2 中的每个元素 arr2[i] 都出现在 arr1 中

```





#### Analysis

数组的重新排序, 首先一定需要一个新数组, 在这里要一个和 arr1 相同长度的新数组.

接着, 以 arr2 的顺序为标准, 将 arr2 的值依次赋值给 newArr, 这里会调用上 findFrequency 连续赋值 frequency 次, 下一次从 i+frequency+1 的位置开始接着赋值(将 arr2 中的依次赋值到 newArr 中.)

原来我少了将 arr1 中多余元素取出排序赋值的步骤.

另外建一个方法 findFrequency 专门用来查找一个数字在另一个数组中出现的个数. 然后把这个结果用在给新数组赋值上.



##### commit 1

0个通过

```java
class Solution {
    public int[] relativeSortArray(int[] arr1, int[] arr2) {
        int temp;   //  用于做交换位置的中间值
        int[] newArr = new int[arr1.length];    //  重新排位
        //  两个数组都要遍历, 以第二个为标准, 在第一个中找频数, 并搬运到对应的位置
        
        int m = 0;  //  arr2 的自增量
        int n = 0;  //  newArr 的自增量
        while (m < arr2.length) {
            int frequency = findFrequency(arr1, arr2[m]);            
            for (int i = 0; i < frequency; i++) {
                //  把arr2中当前的第m位赋值给newArr, 有多少个连续赋值多少个, 下次从 m+frequency+1 开始
                newArr[i] = arr2[m];                
            }
            m++;
            n = n+frequency+1;      //  下一次从跳过的位置开始加
        }                    
        return newArr;
    } 

    //  找出指定元素在一个数组中出现的频数, 这将会作为排序的一个指标. 返回多出的个数.
    public int findFrequency(int[] arr, int x) {
        int count = 0;
        for (int i = 0; i < arr.length; i++) {
            if(arr[i] == x) {
                count++;
            }
        }
        return count;  
    }
}
```



```
输入：
[2,3,1,3,2,4,6,7,9,2,19]
[2,1,4,3,9,6]
输出：
[6,3,2,0,0,0,0,0,0,0,0]
预期结果：
[2,2,2,1,4,3,3,9,6,7,19]
```



在经过分析的整理后, 在规定的时间前, 伪代码列出如下.

```java
class Solution {
    public int[] relativeSortArray(int[] arr1, int[] arr2) {
        int temp;   //  用于做交换位置的中间值
        int[] newArr = new int[arr1.length]();    //  重新排位
        //  两个数组都要遍历, 以第二个为标准, 在第一个中找频数, 并搬运到对应的位置
        
        int m = 0;  //  arr2 的自增量
        int n = 0;  //  newArr 的自增量
        while (m < arr2.length) {
            int frequency = findFrequency(arr1, arr2[m]);            
            for (int i = 0; i < frequency; i++) {
                //  把arr2中当前的第m位赋值给newArr, 有多少个连续赋值多少个, 下次从 m+frequency+1 开始
                newArr[i] = arr2[m];                
            }
            m++;
            n = n+frequency+1;      //  下一次从跳过的位置开始加
        }                    
        return newArr;
    } 

    //  找出指定元素在一个数组中出现的频数, 这将会作为排序的一个指标. 返回多出的个数.
    public int findFrequency(int[] arr, int x) {
        int count = 0;
        for (int i = 0; i < arr.length; i++) {
            if(arr[i] == x) {
                count++;
            }
        }
        return count;  
    }

    //  分出两个数组的差集, 并将差集进行排序, 返回一个由差集组成的升序数组. 返回一个可以依次赋值给 newArr 的小数组
    public int[] restArr(int[] arr1, int[] arr2) {
        int[] rest = new int[arr1.length - arr2.length]();
        //  查找
        //  移动赋值
        //  排序
        return rest;
    }
}
```

> 将缺少的部分另外新建一个新的方法完成
>
> 该方法用于找出两个数组的差集, 并将差集排好序, 返回一个排好序的数组
>
> 主方法中在完成对 arr2 的按频赋值后就调用这个方法完成剩余的步骤.



#### 答案

```java
class Solution {
    public int[] relativeSortArray(int[] arr1, int[] arr2) {
        int[] nums = new int[1001];
        int[] res = new int[arr1.length];
        //遍历arr1,统计每个元素的数量
        for (int i : arr1) {
            nums[i]++;
        }
        //遍历arr2,处理arr2中出现的元素
        int index = 0;
        for (int i : arr2) {
            while (nums[i]>0){
                res[index++] = i;
                nums[i]--;
            }
        }
        //遍历nums,处理剩下arr2中未出现的元素
        for (int i = 0; i < nums.length; i++) {
            while (nums[i]>0){
                res[index++] = i;
                nums[i]--;
            }
        }
        return res;
	}
}
```

