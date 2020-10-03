#### Question [单调数列](https://leetcode-cn.com/problems/monotonic-array/)/[Monotonic Array](https://leetcode-cn.com/problems/monotonic-array/)

tag#array#



#### Description

```
如果数组是单调递增或单调递减的，那么它是单调的。

如果对于所有 i <= j，A[i] <= A[j]，那么数组 A 是单调递增的。 如果对于所有 i <= j，A[i]> = A[j]，那么数组 A 是单调递减的。

当给定的数组 A 是单调数组时返回 true，否则返回 false。

 

示例 1：

输入：[1,2,2,3]
输出：true
示例 2：

输入：[6,5,4,4]
输出：true
示例 3：

输入：[1,3,2]
输出：false
示例 4：

输入：[1,2,4,5]
输出：true
示例 5：

输入：[1,1,1]
输出：true
 

提示：

1 <= A.length <= 50000
-100000 <= A[i] <= 100000

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/monotonic-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```



#### Analysis

题目很明了, 和单调数列有关的.

结合题目的描述可知, 单调性是非递减或者非递增即可.

所以题目很直接.

拿升序排好的数组和原数组正着匹配一遍, 然后再逆着匹配一遍, 两种情况有一种成立, 即符合条件.

> 如果给定的数组和排序后的数组在面前, 一个从前往后走, 另一个从后往前走, 依次两两相等, 那么两个数组明显逆序. 换句话说. 与升序后的数组满足**逆序相等**的它一定是按着降序排列的.
>
> 如
>
> [1,2,3,3,4]
>
> [4,3,3,2,1]



##### 方法

结合 Java 中 Arrays 的 API - Arrays.sort(type[] arr): void,

对原数组来一遍就可以开始比对了. 当然, 由于它是对原数组 "就地" 排序的, 所以提前对原数组作个拷贝, 以为后面的比对作保留.

拷贝的 API - Arrays.copyOf(type[] a): type[] b.

至于接下来的匹配部分, 有两个技巧:

1.正方向的比对可以用 Arrays 的 equals(type[] a, type[] b): boolean. 这个 API 只要两个数组元素类型相等, 元素值也一一对应相等即返回 true.

2.反方向的匹配判等可以循环遍历, 拿一个数组的第 `i` 位与另一个数组的第 `arrB[arrB.length - i + 1]` 比较.

如果说明从头到尾都相等呢, 引入一个布尔值, 初始值设为 `true`. 再条件判断设为 `if(arrA[i] != arrB[arrB.length - i + 1])` 时才修改布尔值, 最后对布尔值检验, 若布尔值没经过修改说明就没遇到过这种情况, 一直为 `true`.

若以上两种情况有一种为 `true` 就可以返回了. 否则返回 `false`.



#### Code

commit 1

```java
class Solution {
    public boolean isMonotonic(int[] A) {        
        int[] B = Arrays.copyOf(A, A.length);
        Arrays.sort(A);
        //  当两个数组完全相等时返回 true
        if (Arrays.equals(A, B) == true)
            return true;
        boolean always = true;
        //  当两个数组不存在不相等的元素时, 返回 true
        for (int i = 0; i < A.length; i++) {
            if (B[A.length - i -1] != A[i])
                always = false;
        }
        if (always)
            return true;
        //  否则返回 false
        return false;
    }
}
```



效果:

```
执行结果：通过 显示详情
执行用时：10 ms, 在所有 Java 提交中击败了6.73%的用户
内存消耗：47.5 MB, 在所有 Java 提交中击败了83.96%的用户
```





