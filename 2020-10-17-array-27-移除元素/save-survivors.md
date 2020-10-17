#### Question [27. 移除元素](https://leetcode-cn.com/problems/remove-element/)

tag#数组# #原地修改#



#### Description

```
给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素，并返回移除后数组的新长度。

不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并 原地 修改输入数组。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

 

示例 1:

给定 nums = [3,2,2,3], val = 3,

函数应该返回新的长度 2, 并且 nums 中的前两个元素均为 2。

你不需要考虑数组中超出新长度后面的元素。
示例 2:

给定 nums = [0,1,2,2,3,0,4,2], val = 2,

函数应该返回新的长度 5, 并且 nums 中的前五个元素为 0, 1, 3, 0, 4。

注意这五个元素可为任意顺序。

你不需要考虑数组中超出新长度后面的元素。
 

说明:

为什么返回数值是整数，但输出的答案是数组呢?

请注意，输入数组是以「引用」方式传递的，这意味着在函数里修改输入数组对于调用者是可见的。

你可以想象内部操作如下:

// nums 是以“引用”方式传递的。也就是说，不对实参作任何拷贝
int len = removeElement(nums, val);

// 在函数里修改输入数组对于调用者是可见的。
// 根据你的函数返回的长度, 它会打印出数组中 该长度范围内 的所有元素。
for (int i = 0; i < len; i++) {
    print(nums[i]);
}

```



#### 效果: 将近双 100 解




#### Analysis

一开始看到这道题的时候就想到压缩数组. 

当然, 如果只是返回除了和 `val` 相等的项的项的个数的话, 一个计数器就可以搞定了. 但是返回的测试用例直接把我给遣返了了. [第一次 commit]

> 大致就是说只是单纯对其它值计数但是并没有替换到前 result 位的意思

这就更像是压缩数组了, 一定要将其它值替换掉所有"出现"的 `val` , 并且让他们出现在前 result 位. (根据题目反复提示的下面两句话也可以得出这一结论)

> **注意这五个元素可为任意顺序。**
>
> **你不需要考虑数组中超出新长度后面的元素。**

所以问题就是一个将一个排序数组("相同的"集中在一起就方便替换了)中炸弹值(姑且就这样称呼 val 吧)后面的数据从炸弹值开始的地方, 都安排到前面来.

所以这个接近双 100 的答案就这么来的.

因为题目只说了 O(1) 的限制, 并没有规定说不能用 T(n), 所以就多用了几次 for 循环. 加上, 零零散散的计数器变量又不影响空间复杂化度的数量级.

![](https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-10-17-array-27-%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0/save-data-behind-booms.jpg)


#### Code

```java
class Solution {
    // 执行用时：1 ms, 在所有 Java 提交中击败了100.00%的用户
    // 内存消耗：36.8 MB, 在所有 Java 提交中击败了99.69%的用户
    public int removeElement(int[] nums, int val) {
        int count = 0;        
        int restCount = 0; 
        Arrays.sort(nums);
        int pos = 0;
        int len = nums.length;  
        //	计算开始位置的
        for (int i=0; i<len; i++) {
            if (nums[i] == val) {
                pos = i;
                break;
            }
        } 
        //	计算出现次数的
        for (int i=pos; i<len; i++) {
            if (nums[i] == val) {
                count++;
            }                            
        }  
        //	排除刚好后面都是 val 值的
        if (pos+count == len) 
            return pos; 
        //	将后面幸存的数据都救回来
        for (int j=pos+count; j<len; j++) {
            nums[j-count] = nums[j];
            restCount++;
        }
        return pos+restCount;
    }
}
```





有点像拯救后面幸存的战士一样.

像 {1, 2, 2, 2, 3, 4, 5} 炸弹值为 2 的时候, 后面的 {3, 4, 5} 就是无辜的战士了. 必须把他们给救回来.



