#### Question [剑指 Offer 59 - I. 滑动窗口的最大值](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)

tag#剑指 offer# #滑动窗口#



#### Description

```
给定一个数组 nums 和滑动窗口的大小 k，请找出所有滑动窗口里的最大值。

示例:

输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
输出: [3,3,5,5,6,7] 
解释: 

  滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
 

提示：

你可以假设 k 总是有效的，在输入数组不为空的情况下，1 ≤ k ≤ 输入数组的大小。
```

注意：本题与主站 239 题相同：https://leetcode-cn.com/problems/sliding-window-maximum/



#### Analysis

滑动窗口, 移动 low. 其中窗口移动的终点可以拿 nums.length=5, k=3 为例具体化.



#### Code

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        // 执行用时：34 ms, 在所有 Java 提交中击败了17.99%的用户
        // 内存消耗：46.6 MB, 在所有 Java 提交中击败了79.13%的用户
        int len = nums.length;
        // i. 长度为 0, 返回[]
        if (len == 0 || len < k)
            return new int[]{};
        //  ii. 长度不为 0, k 为 1, 返回nums本身. (每一个都是最大的)
        if (k == 1)
            return nums;        
        int newLen = len - k + 1;   //  newArr 的长度总比 nums 少 k-1; 如 5, 3, newLen 为 3
        int[] newArr = new int[newLen];
        // 遍历数组, 令 low 等于当前的 i, 循环终点设为 len-k; 如 5, 3, 终点为 2.
        for (int i=0; i<=len-k; i++) {  //  这里的循环终点设为 len-k, 如 len=5, 循环到第 3 位也就是 i=2
            int low = i;    
            int high = i+k-1;           // 每次令 high 为 low 后 (k-1) 的位置
            int max = nums[i];  
            while (low < high) {     //  如 0<3                              
                low++;               //  打擂台
                if (nums[low] > max) {
                    max = nums[low];                    
                }
                newArr[i] = max;     //  nums[i] 与 newArr[i] 一一对应
            }
        }
        return newArr;
    }
}
```







