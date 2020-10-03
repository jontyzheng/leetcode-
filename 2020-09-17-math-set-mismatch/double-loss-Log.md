#### Question 错误的集合/[645. Set Mismatch](https://leetcode-cn.com/problems/set-mismatch/)

tag#math#



#### Description

```
集合 S 包含从1到 n 的整数。不幸的是，因为数据错误，导致集合里面某一个元素复制了成了集合里面的另外一个元素的值，导致集合丢失了一个整数并且有一个元素重复。

给定一个数组 nums 代表了集合 S 发生错误后的结果。你的任务是首先寻找到重复出现的整数，再找到丢失的整数，将它们以数组的形式返回。

示例 1:

输入: nums = [1,2,2,4]
输出: [2,3]
注意:

给定数组的长度范围是 [2, 10000]。
给定的数组是无序的。
```



#### Analysis

题意分析: 给定一个**无序**的数组 (这一点在"注意"部分中给出). 只有从 1 开始递增, 直到最后一个才算是满足"正确的集合". 已知有一项复制了另外一项, 导致另一个数子消失.

这个消失的项有可能是复制值中的其中一个. `1, 2, 2, 4`

也有可能是完全被排出的一项. 如 `2, 2, 3`

现在要求返回一个长度为 2 的数组. 要求第一个是重复的那个项. 第二个是因为重复而消失的一项.

解题分析:

注意用例:

[2, 3, 3, 4, 5, 6] 因为 3 重复导致 2 消失. 这时候消失的项**既不在重复的正前面, 也不是重复元素的正后面.**

#### Code

```java
class Solution {
    public int[] findErrorNums(int[] nums) {
        
        int[] counter = new int[nums.length+1];
        
        for (int i: nums) {
            counter[i]++;
        }
        
        int[] result = new int[2];
        for (int i = 1; i<counter.length; i++) {
            if (counter[i] == 0) {
                result[1] = i;
            } else if (counter[i] == 2) {
                result[0] = i;
            }
        }
        
        return result;
    }
}
```

> 摘自评论区

效果:

执行用时：2 ms, 在所有 Java 提交中击败了96.14%的用户

##### commit 1

```java
class Solution {
    public int[] findErrorNums(int[] nums) {
        int len = nums.length;
        int[] result = new int[2];
        Arrays.sort(nums);
        //  从 1 递增的数组中, 有一项复制了另一个项. 则实际上错误的只有一个元素.
        //  现要求这两个值. 包括没错的那一项, 以及复制了他人的那一项.        
        for (int i = 0; i < len; i++) {
            //  由于数组一定是从 1 开始递增到最后一个的数组, 所以这里拿初始值为 0 的 i+1 进行匹配
            if (nums[i] != (i+1)) {
                //  实际上只会有一项不匹配. - (连续重复)                
                //  不匹配的有两种情况:
                //  1.如果和前面重复, 就说明向下兼容. 此时对应的是返回数组的第二项 result[1]. 第一项为原来的值.
                if ( nums[i] < (i+1)) {                    
                    result[0] = nums[i];
                    result[1] = nums[i]+1;    //  后一项
                } 
                //  2.如果和后面的重复, 就说明向上兼容. 此时对应的是返回数组的第一项 result[0]. 第二项为 i+1;
                else {
                    result[0] = nums[i];
                    result[1] = nums[i]-1;
                }                                
            }
        }
        return result;
    }
}
```

> 未通过.







