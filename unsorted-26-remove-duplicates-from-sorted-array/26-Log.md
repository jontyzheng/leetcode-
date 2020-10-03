### Question Title: Remove Duplicates from Sorted Array

#tag# array

### Description

```
给定一个排序数组，你需要在 原地 删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。

 

示例 1:

给定数组 nums = [1,1,2], 

函数应该返回新的长度 2, 并且原数组 nums 的前两个元素被修改为 1, 2。 

你不需要考虑数组中超出新长度后面的元素。
示例 2:

给定 nums = [0,0,1,1,1,2,2,3,3,4],

函数应该返回新的长度 5, 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4。

你不需要考虑数组中超出新长度后面的元素。

```

### Analysis

key words: **modifying the input array in-place**

Well, I gotta say, this question took me almost two hours and finally got the answer from the serveral different versions that other coder provided.

At first glance, What I thought is to iterate every item in the array given and do some comparing and replacing things.

However, when I listed the situation like something likes below, I finally find the key step which also the most important process of solution.

e.g. {0, 0, 1, 1, 1, 2}

To make sure all the duplicates being removed form the array, I listed every single process to make them clearer.

0 0 1 1 1 2

0 1 1 1 2

0 1 1 2

0 1 2

Yeah, comparing from the second one until there is no more value of item beging same as the first one.
Then, changing the starter of the iteration and do the same thing. I gotta say, That did be how I think it as the first time.

However, I find something wrong with that, if only to compare once and do the replacing work, those operations would only being did one round, then turn the starter changing work.

So there the question is,what if the array is {0, 0, 0, 1, 1}.

0 0 0 1 1

0 0 1 1

0 1 1

Right? If the first value appears three times in the row, with the second compare-replace work done, when it comes to the third step, still, the first value is needed to be compared, which is for checking out no more same values being same as it.

So, I turn to the comment area, at which I have read serveral answer but got confused about them. All of them uses the <I>while</I> and alse the nums[++i] or other thing like that. Then I finally found the straighway answer:

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length < 1) 
            return 0;
        if (nums.length == 1)
            return 1;
        
        int n = 0;  //  n: 最开始的被比较对象, 若从第二个开始遇到不同的就更新
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] != nums[n]) {
                n++;    
                nums[n] = nums[i];  
            }
        }
        return n+1;
    }
}
...

Yeah, that is the version I updated my original answer on the base of the answer solution, the original solution simplifies the former two steps above, which I believe u must know what it is.

The core step is **the replacing part in-place**, yeah, that does change completely the original array. 

Firstly, it create a new varible named n, which is 0 originally. That is the substitution of numa[0].

when there is no more same value equaling the nums[n], n gotta update, and also, make the different one to replae it!
In the first round, n = 0, if the nums[1] is not as same as the nums[n] in value, n gotta updated, which turns the following one, and make the nums[n] nums[i], the item beging used to compare.


To be contunue..
