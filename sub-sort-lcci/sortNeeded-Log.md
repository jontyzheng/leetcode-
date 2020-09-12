#### Question 部分排序/[Sub Sort LCCI](https://leetcode-cn.com/problems/sub-sort-lcci/)

tag#sort#



#### Description

```
给定一个整数数组，编写一个函数，找出索引m和n，只要将索引区间[m,n]的元素排好序，整个数组就是有序的。注意：n-m尽量最小，也就是说，找出符合条件的最短序列。函数返回值为[m,n]，若不存在这样的m和n（例如整个数组是有序的），请返回[-1,-1]。

示例：

输入： [1,2,4,7,10,11,7,12,6,7,16,18,19]
输出： [3,9]
提示：

0 <= len(array) <= 1000000
```





#### Analysis

题意分析: 由题可得, 题目想找的就是: 为了让给定数组升序排列, 需要**动**的最小区间. 所以题目还可以命名叫 "求升序的最小需要动用部分".

也就是实际需要排序的那部分. 虽然说也不存在什么最小区间, 只要和排好序的数组两头有一个不一样, 那么从那里开始到中间, 就是需要真正排序的区间.

解题分析:

理解了题目是找需要排序的区间后, 首先想到的就是找与排好序后的数组, **开始不一样**的地方. 因为 `Arrays.sort(Object[] array)` 会将原数组就地排序, 所以对原数组做了一份复制, 再让它变成排序后对照的数组. 之后比对匹配查找即可.



#### Code

##### commit 1

解是解出来了, 说明思路没偏.

但是我知道其实是用了两个最笨的方法找头尾的坐标 `i`, `j`.

为了找到数组头尾第一个与 `cpArr` 不同的索引, 用了 2 个 `for` 循环, 然后 `break` 出来.

```java
class Solution {
    public int[] subSort(int[] array) {
        int len = array.length;
        int[] result = new int[2];
        int[] cpArr = new int[len];
        //  复制数组 cpArr
        for (int i = 0; i < len; i++) {
            cpArr[i] = array[i];
        }     
        //   数组排序
        /*for (int i = 0; i < len; i++) {            
            for (int j = 1; j < len; j++) {
                if (cpArr[j] > cpArr[i]) {  
                    int temp = 0;
                    temp = cpArr[i];
                    cpArr[i] = cpArr[j];    
                    //冒泡排序 实际上每一对数都相互比较过了, 如果它比原来位上的元素小的话
                    cpArr[j] = temp;
                }
            }
        }
        */
        Arrays.sort(cpArr);
        
        boolean same = true;
        //	从头开始找第一个不一样的
        for (int i = 0; i < len; i++) {
            if (array[i] != cpArr[i]) {
                result[0] = i;
                break;
            }
        }
        //	从尾巴开始找第一个不一样的
        for (int j = len-1; j >= 0; j--) {
            if (array[j] != cpArr[j]) {
                result[1] = j;
                break;
            }
        }
        if ( result[0] == 0 && result[1] == 0) {
            result[0] = -1;
            result[1] = -1;
        } 
        return result;
    }
}
```

效果:

执行用时：21 ms, 在所有 Java 提交中击败了21.13%的用户

##### 可以改进的地方

> 如果找到的区间端点值是 `[0, 0]`, 说明没找到, 原数组不变, 按照题目的要求, 修改成 `[-1, -1]` 返回.
>
> 与"将原区间数组就设置为`[-1, -1]` 之后的查找成功就当作是更新数组, 最后返回数组" 其实属于不同的两种思路, 都可以.

 `result` 将结果数组的初始值设为 `[-1, -1]`, 之后的找到当作成对数组内的值更新, 最后返回无论又找到还是没找到都可以返回区间数组.  



commit 2

commit 3





