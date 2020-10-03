#### Question [922. 按奇偶排序数组 II](https://leetcode-cn.com/problems/sort-array-by-parity-ii/)/[Sort Array By Parity II](https://leetcode-cn.com/problems/sort-array-by-parity-ii/)

tag#sort# #array#



#### Description

给定一个非负整数数组 A， A 中一半整数是奇数，一半整数是偶数。

对数组进行排序，以便当 A[i] 为奇数时，i 也是奇数；当 A[i] 为偶数时， i 也是偶数。

你可以返回任何满足上述条件的数组作为答案。

 

示例：

```
输入：[4,2,5,7]
输出：[4,5,2,7]
解释：[4,7,2,5]，[2,5,4,7]，[2,7,4,5] 也会被接受。
```



提示：

1. 2 <= A.length <= 20000
2. A.length % 2 == 0
3. 0 <= A[i] <= 1000



#### Analysis

题意分析: 已知给定的数组是一个由非负整数组成的数组了. 其中有一半是奇数, 另一半是偶数. 现在要返回一个数组, 要求是奇数位上是奇数, 偶数位上是偶数.

如 给定数组为 `[4, 2, 5, 7]` 满足条件的可以是 `[2, 5, 4, 7]` 也可以是 `[4, 7, 2, 5]` 诸如此类的.

解题分析: 把原数组奇数的项放到一个奇数数组里, 偶数的项放到一个偶数数组里. 然后再遍历, 判断循环因子: 当奇数的时候就赋值奇数数组里的值, 偶数时就复制偶数数组里的值.



#### Code

须知: 需要注意的是, 奇偶数数组和赋值的时候用不同的迭代因子, 而且要控制好它们不会越界.

```java
class Solution {
    public int[] sortArrayByParityII(int[] A) {
        //  长度默认为 2, 且奇偶数各占一半
        int len = A.length;
        int[] even = new int[len/2];
        int[] odd = new int[len/2];
        int j = 0;
        int k = 0;
        for(int i = 0; i < len; i++) {
            if (A[i] % 2 == 0) {
                //  先赋值, 再加加
                even[j] = A[i];
                j = (j < len/2-1) ? j+1 : j;
            }
            //  if 括号外的默认是一定执行的代码.
            else {
                odd[k] = A[i];
                k = (k < len/2-1)? k+1 : k;  //  只要还在长度范围内就可以加加
            }
            
        }
        //  得到奇数数组和偶数数组后, 按照 i 的奇偶性重新赋值到新的数组
        int[] result = new int[len];
        int x = 0;
        int y = 0;
        for (int i = 0; i < len; i++) {
            if (i%2 == 0) {
                result[i] = even[x];
                x = (x < len/2-1)? x+1 : x;
            }
            else {
                result[i] = odd[y];
                y = (y < len/2-1)? y+1 : y;
            }            
        }
        return result;
    }
}
```

效果:

执行结果：

通过

显示详情

执行用时：4 ms, 在所有 Java 提交中击败了33.61%的用户

内存消耗：43.4 MB, 在所有 Java 提交中击败了6.09%的用户







