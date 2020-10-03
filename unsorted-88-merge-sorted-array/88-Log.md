### Question title: [Merge Sorted Array](https://leetcode-cn.com/problems/merge-sorted-array/)



> Well, I gotta say, I've seen this title before, so I have impression of it.



### Description

```
Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

Note:

The number of elements initialized in nums1 and nums2 are m and n respectively.
You may assume that nums1 has enough space (size that is equal to m + n) to hold additional elements from nums2.
Example:

Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
 

Constraints:

-10^9 <= nums1[i], nums2[i] <= 10^9
nums1.length == m + n
nums2.length == n
```



### Analysis

As the *constrains* part says, 

nums1 is a array with length are the sum of both array, which means that nums1 is able to contain the second array, in other words, nums2 could absolutely be put into nums1. Yeah, this is what I think at first time I saw it.



### Code

##### The code committed at the first time

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        //  如果 nums1 足够长
        int j = 0;
        for (int i = m; j < n; i++) {
            nums1[i] = nums2[j];
            j++;
        }
        Arrays.sort(nums1);
    }
}
```

Yes, I have though about the selection sort but I did not do it in one go, then it reminds of the Java API.



#### A better version

However, what the meaning of algorithm left if everyone do it in this way, so I started to find out better strategies.



Then this solution caught my eyes.

> Execution time: 1 ms, beating 99.05% of user memory consumption: 34.8 MB, beating 95.46% of users
>
> ```java
> public void merge(int[] nums1, int m, int[] nums2, int n) {
>  int i = m--+--n;
>      
>  while(n>=0) {
>      nums1[i--] = m>=0 && nums1[m]>nums2[n] ? nums1[m--] : nums2[n--];
>  }
> }
> ```



Looks pretty clean, It looks like demolishing  and resetting. 

As we know, it is quite certain that the nums1 is able to hold the later one, which means, the length of nums1 is the sum of both of them. Let's make it in this way, array nums1 have enough space to hold both of them.



Yeah, It's not no long talking about how to put the later array into nums1, It's talking about how to reset the nums1, in cleaner way, how to reset the item in the nums1.



So that is much cleaner, the solution turns into how to reset the item in the nums1, more concret, how to reset the values of items in the nums1.



##### The code committed at the first time

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int i = m + n - 2;		/*something went wrong*/

        while (n >= 0) {
            nums1[i--] = m>=0 && nums1[m] > nums2[n] ? nums1[m--] : nums2[n--];
        }
    }
}
```



result

```
执行出错信息：
Line 6: java.lang.ArrayIndexOutOfBoundsException: Index 3 out of bounds for length 3
最后执行的输入：
[1,2,3,0,0,0]
3
[2,5,6]
3
```



Why I got ArrayIndexOutOfBoundsException? It turn out that because the value of i represents is far more than the item in the array, even the nums1. Yeah, the i is actually two less than the sum of m&n, but it ignores the expression below.

```java
nums1[i--] = m>=0 && nums1[m] > nums2[n] ? nums1[m--] : nums2[n--];
```

> Neither nums1[m] or nums2[n] could represent nothing.

So we gotta adjust these two values, m & n.

Watching the code at this time, I got why it write the first step in this way.

It merges the two step into one, the initialization of i and the adjustment of m&n.

> m--: update after the expression is executed (which is not affect the initialization of i)
>
> --n: 

To be continue..
