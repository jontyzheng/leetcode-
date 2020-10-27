#### Question [303. 区域和检索 - 数组不可变](https://leetcode-cn.com/problems/range-sum-query-immutable/)

tag#数组# #缓存#



#### Description

```
给定一个整数数组  nums，求出数组从索引 i 到 j（i ≤ j）范围内元素的总和，包含 i、j 两点。

实现 NumArray 类：

NumArray(int[] nums) 使用数组 nums 初始化对象
int sumRange(int i, int j) 返回数组 nums 从索引 i 到 j（i ≤ j）范围内元素的总和，包含 i、j 两点（也就是 sum(nums[i], nums[i + 1], ... , nums[j])）
 

示例：

输入：
["NumArray", "sumRange", "sumRange", "sumRange"]
[[[-2, 0, 3, -5, 2, -1]], [0, 2], [2, 5], [0, 5]]
输出：
[null, 1, -1, -3]

解释：
NumArray numArray = new NumArray([-2, 0, 3, -5, 2, -1]);
numArray.sumRange(0, 2); // return 1 ((-2) + 0 + 3)
numArray.sumRange(2, 5); // return -1 (3 + (-5) + 2 + (-1)) 
numArray.sumRange(0, 5); // return -3 ((-2) + 0 + 3 + (-5) + 2 + (-1))
 

提示：

0 <= nums.length <= 104
-105 <= nums[i] <= 105
0 <= i <= j < nums.length
最多调用 10^4 次 sumRange 方法
```



#### Analysis

重要的信息是会调用很多次 sumRange.

每调用一次就是 O(n) 次.

方法: 缓存数组中从 0 到第 k 项的和. 当要找 i - j 之间的数组元素和时, 可以返回前 j 项的 sum 和前 i 项的差.

用一个数组缓存这样的和.

其中, 用累加的方式, 从第一项开始, 将依次累加的和放在后一位. 这样, 从第二项开始, 第二项存放的是第 1 项和第 2 项的和. 第三项开始, 后一位加上前一项, 也就是累加上前 2 项的和, 依次类推可以得到, 第 k 项就是从第 0 到 第 k 项的元素和.

由于最后还有一位记录前 nums.length - 1 项的和, 所以新数组的长度要比原数组的长度加 1. 以存放这一个和.

在调用 sumRange(i, j) 中返回 sums[j] - sums[i] 即可得到已经计算好的求和. 时间复杂度为 O(1).



#### Code

```java
class NumArray {
    // 执行用时：9 ms, 在所有 Java 提交中击败了99.83%的用户
    // 内存消耗：41.2 MB, 在所有 Java 提交中击败了95.46%的用户
    int[] sums;


    public NumArray(int[] nums) {
        sums = new int[nums.length+1];
        for (int i=0; i<nums.length; i++) {
            sums[i+1] = sums[i] + nums[i];
        }
    }
    
    public int sumRange(int i, int j) {
        return sums[j+1] - sums[i];
    }
}

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray obj = new NumArray(nums);
 * int param_1 = obj.sumRange(i,j);
 */
```



##### 数组缓存, 真的, 不愧为官方题解.



