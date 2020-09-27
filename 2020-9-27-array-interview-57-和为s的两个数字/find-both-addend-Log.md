#### Question [在升序的正数数组中找给定目标值的两个加数](https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/)

tag#剑指 offer# #array# 



#### Description

```
输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可。

 

示例 1：

输入：nums = [2,7,11,15], target = 9
输出：[2,7] 或者 [7,2]
示例 2：

输入：nums = [10,26,30,31,47,60], target = 40
输出：[10,30] 或者 [30,10]
 

限制：

1 <= nums.length <= 10^5
1 <= nums[i] <= 10^6
```



#### Analysis

建立字典, 为所有小于目标值的元素建立字典, 加数(当前项)为 key, 差数为 value. 如果存在这样的加数对的话, 通过 value 为 key 拿到的 value 不为空.

即假设两个加数之和确定, 一个加数的差值等于差值的差值. 在以加数为 key, 差值为 value 的字典中, 总可以找到 value 对应的另一组键值对.

由于数组元素都为正整数, 加数不可能为负数, 所以任意一个加数都不可能超过两数之和(目标值), 所以只需要给小于目标值的元素建立字典. 特别是已知升序的情况下, 遇到大于两数之和的数值就不能管它们了.

#### Code

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        // 执行用时：90 ms, 在所有 Java 提交中击败了5.35%的用户
        // 内存消耗：49.3 MB, 在所有 Java 提交中击败了98.93%的用户
        int len = nums.length;
        int[] result = new int[2];        
        Map<Integer, Integer> map = new HashMap<>();
        if (len < 2 || nums[0] > target)
            return null;
        int mid = 0;
        // 只给小于 target 的元素建立字典索引.
        for (int i=0 ;i<len; i++) {
            if (nums[i] < target) {
                map.put(nums[i], target-nums[i]);
            }                        
        }
        int size = map.size();  
        for (int i=0; i<size; i++) {
            int diff = map.get(nums[i]).intValue();
            if (map.get(diff) != null) {
                result[0] = nums[i];
                result[1] = target - nums[i];                                                
                break;
            }            
        }
        return result;
    }
}
```



##### commit 1

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        // 27 / 36 个通过测试用例
        // 执行结果：超出时间限制
        int len = nums.length;
        int[] result = new int[2];        
        
        if (len < 2 || nums[0] > target)
            return null;
        int mid = 0;        
        for (int i=0 ;i<len; i++) {
            if (nums[i] > target/2) {
                mid = i+1;
                break;
            }
        }
        for (int i=0; i<mid; i++) {
            int diff = target - nums[i];
            for (int j=i+1; j<len; j++) {
                if (nums[j] == diff) {
                    result[0] = nums[i];
                    result[1] = nums[j];
                }
            }
        }
        return (target != 0 && result[0] != 0)? result:null;
    }
}
```





