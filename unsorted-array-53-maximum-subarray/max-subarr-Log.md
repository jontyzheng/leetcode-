#### Question [最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)/[Maximum Subarray](https://leetcode-cn.com/problems/maximum-subarray/)

tag#array#



#### Description

```
给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

示例:

输入: [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
进阶:

如果你已经实现复杂度为 O(n) 的解法，尝试使用更为精妙的分治法求解。

```



#### Analysis





**5 / 202** 个通过测试用例

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {
            outer:
            if (nums[i] > 0) {
                sum += nums[i];
                int negSum = 0;     //  每次新起点往后有效
                //  起点
                for (int j = i+1; j < nums.length; j++) {   
                    int negNum = 0;
                    while (nums[j] < 0) {
                        //  在遇到下一个正数前, 累加可能出现的复数
                        negNum++;                        
                        negSum += nums[j];
                        if (Math.abs(negSum) >= sum) {
                            break outer;        //  重新选取起点
                        }                                            
                        j++;        
                    }            
                    if (negNum == nums.length-j)     // 当后面出现都是负数时返回到目前为止累计的sum
                        return sum;
                    sum += nums[j];             //  否则, 继续累加正数
                    //  如果这时候又遇到后面都是负数呢?
                }
            }
        }
        return sum;        
    }
}
```



由整个流程可知, 最好的情况是从 0 开始计算.

数组排列所有的情况有以下四种:

1. all 负数
2. all 正数
3. 负开头, 有正
4. 正开头, 后有负

数学计算中, 第一种和第三种显然有些不必要累加的部分. 部分决定是从第一个正数开始累加才有意义, 和最大的子串一定是以一个正数开头的.

所以 1 和 3 可不考虑.



结合第一次 commit 的代码, 忽然, 这个时候, 如果不那么考虑效率的话, 直接从第一个开始, 也是可以的, 只要 sum 归零. 这样也不会影响后面的计算. 也避免了后面因为 "被减没了 " 而重新"找起点" (其实也是 sum 归零.)



**92 / 202** 个通过测试用例

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int sum = 0;

        for (int i = 0; i < nums.length; i++) {                    
            sum+=nums[i];
            if (sum <= 0) {
                sum = 0;        //  归零
                continue;       //  提前结束
            }            
        }
        return sum;
    }
}
```

> 虽然在累加前也可以直到遇到第一个正数才开始累加, 但是如果有负数校验的话, 只要是负数就会归零.



测试用例

```
输入：
[-2,1,-3,4,-1,2,1,-5,4]
输出：
5
预期：
6
```

> 在累加到本来为 6 的时候, 因为 +(-5)+(4) 实际上还是损失了 1.
>
> 提前结束



后面的负数不会完全剪掉当前的和, 不会让当前SUM减没, 但是在后面的正数加上又得不偿失.

提前返回, 要可以"权衡收益" 决定继续累加.

> 在遇到下一个正数之前存在绝对值更大的负数 or 中间部分的负数之和要大于下一个负数, 而下一负数本身又小于当前累加的sum(不值得重新归零)
>
> 就比如这里的
>
> 在加到 1 的时候sum当前值为 6, 下一个正数为 4.
>
> 加上 5 不会归零, 但是再继续加上 4 的话就得不偿失.
>
> 所以这里要多一个比对, 下一个正数和中间的负数(和)的大小, 权衡后再决定是否继续累加 or 返回当前.



#### 标准答案

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int sum = 0;
        int res = nums[0];  //  暂时假设第一个就是结果
        for (int num:nums) {
            if (sum > 0) {
                sum += num;     //
            }
            else
                sum = num;      //  令sum等于数组内的元素, 等于后比对后还小于 0 的话继续下一个值
            res = Math.max(res, sum);  //   取res和sum中最大的那一个                  
        }
        return res;
    }
}
```

