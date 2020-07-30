### Question: The nums lost

### Description: 

```
一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。

 

示例 1:

输入: [0,1,3]
输出: 2
示例 2:

输入: [0,1,2,3,4,5,6,7,9]
输出: 8
 

限制：

1 <= 数组长度 <= 10000
```

### Analysis
Well, honestly, this question is too kinda easy to write too much annotation.
The array given is definitely in the interval **[0, n - 1]** and in increasing order **with difference of 1**.

But, <I>if the array given start with 1,  which length is absolutely 1. u got '0' lost, which means u gotta return '0'.</I>

Yeah, This is all, knowing the default order requirement, once the array given did not meet the requirement, return the lost one, which is definately one less than the last value in the array.

so, return the lost value, u got it. if not, I mean, the starting with 1 thing having already considered, the array is the right order, we just gotta return the value that one more than the last one in the array.

### Start working

1.Iterate throught the array and ask the difference of two contiguous item whether they got 1 difference in value.

If the answer is not, which means there is one value lost, then we just return lost value, u know, like we have talked above, `nums[i] - 1`, which is also can be `nums[i - 1] - 1`.

else, which means the array is in the right order, then `nums[nums.length - 1] + 1` is the value which needed.

2.Put the "Starting with 1" thing above, which return '0'.

So, here we go.

### Code
```java
class Solution {
    public int missingNumber(int[] nums) {
        int lst = 0;
        //if (nums.length == 1 && nums[0] == 0)
        //  return 1;                           //  下方的默认顺序就包括了这种情况
        if (nums[0] == 1)
            return 0;
        boolean lstOrNot = false;
        for (int i = 1; i < nums.length; i++) {
            if ((nums[i] - nums[i-1]) > 1) {
                lstOrNot = true;
                return nums[i -1] + 1;
            }                            
        }
        if (lstOrNot == false)
            return nums[nums.length - 1] + 1;
        return 0;
    }
}
```

