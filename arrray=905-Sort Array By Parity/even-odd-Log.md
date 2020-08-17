#### Question: [按奇偶排序数组](https://leetcode-cn.com/problems/sort-array-by-parity/)/[Sort Array By Parity](https://leetcode-cn.com/problems/sort-array-by-parity/)



tag#array#



#### Description

```
给定一个非负整数数组 A，返回一个数组，在该数组中， A 的所有偶数元素之后跟着所有奇数元素。

你可以返回满足此条件的任何数组作为答案。

 

示例：

输入：[3,1,2,4]
输出：[2,4,3,1]
输出 [4,2,3,1]，[2,4,1,3] 和 [4,2,1,3] 也会被接受。
 

提示：

1 <= A.length <= 5000
0 <= A[i] <= 5000

```



#### Analysis

只有把负数调到后面即可符合要求



#### Code

```java
class Solution {
    public int[] sortArrayByParity(int[] A) {
        if (A.length == 1)
            return A;
        int t = 0;
        int[] newArr = new int[A.length];

        for (int i = 0; i < A.length; i++) {            
            if (A[i]%2 == 0) {
                newArr[t++] = A[i];
            }        
        }

        for (int i = 0; i < A.length; i++) {
            if (A[i]%2!=0) {
                newArr[t++] = A[i];
            }
        }
        return newArr; 
    }
}
```

> 参考官方解法
>
> 妙啊
>
> 先排一遍偶数再排一遍奇数.
