#### Question [1502. 判断能否形成等差数列](https://leetcode-cn.com/problems/can-make-arithmetic-progression-from-sequence/)/[Can Make Arithmetic Progression From Sequence](https://leetcode-cn.com/problems/can-make-arithmetic-progression-from-sequence/)

tag#sort#



#### Description

```
给你一个数字数组 arr 。

如果一个数列中，任意相邻两项的差总等于同一个常数，那么这个数列就称为 等差数列 。

如果可以重新排列数组形成等差数列，请返回 true ；否则，返回 false 。

 

示例 1：

输入：arr = [3,5,1]
输出：true
解释：对数组重新排序得到 [1,3,5] 或者 [5,3,1] ，任意相邻两项的差分别为 2 或 -2 ，可以形成等差数列。
示例 2：

输入：arr = [1,2,4]
输出：false
解释：无法通过重新排序得到等差数列。
 

提示：

2 <= arr.length <= 1000
-10^6 <= arr[i] <= 10^6
通过次数12,571提交次数16,820
```



#### Analysis

题意分析: 能否形成等差数组, 顾名思义, 判断数组中的项满不满足一个等差数组的条件.

排序后, 两两之间的差值是否相等.

解题分析:

1. 可以专门一个数组盛放两两之间的差值 (排序后), 再以前两个的差值作为标准判断匹配, 有没有不相等的情况.
2. 直接拿前两个元素的差值到原数组中去匹配. (排序后)



#### Code

```java
class Solution {
    public boolean canMakeArithmeticProgression(int[] arr) {
        //  已知至少 2 个元素
        Arrays.sort(arr);
        int len = arr.length;
        //  申请一个用来盛放差值的数组
        boolean hasMeet = true;
        //  不用差数组, 拿第一个元素和第二个元素的差值作为标准, 到原数组中去匹配各个差值: 直到不满足时修改布尔值.
        int tmpDiff = arr[1]-arr[0];
        for (int i = 1; i < len-1; i++) {
            int diff = arr[i+1] - arr[i];
            if (diff != tmpDiff) {
                hasMeet = false;
            }
        }
        return hasMeet;
    }
}
```



##### commit 1

**差数组法**

效果: 执行用时：2 ms, 在所有 Java 提交中击败了17.75%的用户

```java
class Solution {
    public boolean canMakeArithmeticProgression(int[] arr) {
        //  已知至少 2 个元素
        Arrays.sort(arr);
        int len = arr.length;
        //  申请一个用来盛放差值的数组
        int[] diffArr = new int[len-1];
        for (int i = 0; i < len-1; i++) {
            diffArr[i] = arr[i+1]-arr[i];
        }
        int diff = diffArr[0];
        //  验证差值数组的各项相等
        boolean hasMeet = true;
        for (int i = 0; i < len-1; i++) {
            if (diffArr[i] != diff) {
                hasMeet = false;
            }
        }
        return hasMeet;
    }
}
```



##### commit 2

**差匹配法**

效果: 执行用时：1 ms, 在所有 Java 提交中击败了99.30%的用户

```java
class Solution {
    public boolean canMakeArithmeticProgression(int[] arr) {
        //  已知至少 2 个元素
        Arrays.sort(arr);
        int len = arr.length;
        //  申请一个用来盛放差值的数组
        boolean hasMeet = true;
        //  不用差数组, 拿第一个元素和第二个元素的差值作为标准, 到原数组中去匹配各个差值: 直到不满足时修改布尔值.
        int tmpDiff = arr[1]-arr[0];
        for (int i = 1; i < len-1; i++) {
            int diff = arr[i+1] - arr[i];
            if (diff != tmpDiff) {
                hasMeet = false;
            }
        }
        return hasMeet;
    }
}
```







