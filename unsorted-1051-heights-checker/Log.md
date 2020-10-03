## 1051. Heights Checker

#Tag# Array 
#easy#

### Question

```
Students are asked to stand *in non-decreasing order* of heights for an annual photo.

Return the minimum number of students *that must move* in order for all students to be standing in non-decreasing order of height.

Notice that when a group of students is selected they can reorder in any possible way between themselves and the non selected students remain on their seats.

Example 1:

Input: heights = [1,1,4,2,1,3]
Output: 3
Explanation: 
Current array : [1,1,4,2,1,3]
Target array  : [1,1,1,2,3,4]
On index 2 (0-based) we have 4 vs 1 so we have to move this student.
On index 4 (0-based) we have 1 vs 3 so we have to move this student.
On index 5 (0-based) we have 3 vs 4 so we have to move this student.
Example 2:

Input: heights = [5,1,2,3,4]
Output: 5
Example 3:

Input: heights = [1,2,3,4,5]
Output: 0
```
---

### Analysis

1.title reading: The Heights Checker/array

2.Description of this question is talking about *non-deceasing order*, which means something like {1, 1, 2, 3, 4}, {2, 2, 3, 3, 6}, as long as the order is arraged like this.

Then there is another key words -- *find the min of nums that must move*, which means it's not neccessary to actually sort this array.

But I gotta say the real key cue is placed at the *Example* part, more concret, the *Explanation* part.
```
Current array : [1,1,4,2,1,3]
Target array  : [1,1,1,2,3,4]
On index 2 (0-based) we have 4 vs 1 so we have to move this student.
On index 4 (0-based) we have 1 vs 3 so we have to move this student.
On index 5 (0-based) we have 3 vs 4 so we have to move this student.
```

At first glance, I just thought it as in real life, and All we gotta do is just ordering one man to move to another place, the direction is mostly rightward, such as {1, 1, 4, 2, 1, 3} .
Right? when u go the second position and u find the value doesn't meet the requirement, then u gotta move it rightward. '1', '3' are the same thing.

But, when I wrote more sequence to check, I find out that not all the "min of nums that need to move" follow the "rightward" thing, like {1, 1, 4, 3, 1}, which <I>min</I> is 2, and the labor-saving way is put '1' leftward, so as '3' do.

I got little confused. U know, no need to actually sort them, all u have to do just find the times they must move to make them in non-deceasing order, right? But the uncertain direction thing kinda confused me.

So I turn to comments area for other voices,  most voices there are talking about the translation thing, so I just turn it into the en-version, then I got the point.
I mean, I finnaly figure out the Example part, which is already told us the answer.

```
Current array : [1,1,4,2,1,3]
Target array  : [1,1,1,2,3,4]
On index 2 (0-based) we have 4 vs 1 so we have to move this student.
On index 4 (0-based) we have 1 vs 3 so we have to move this student.
```

Yeah, while u comparing one original one to the sorted one, how many different pair u find, how many times u need to move.

So, for that, the non-decreasing order is there. And we also know, there is a method called `Arrays.sort()`, which makes the same order thing. Then we got the idea.

### Start work

1. Using the `Arrays.sort()` to sort the <I>heights</I> firstly. Note that the value it returns is boolean, which means it do sort the original array. So, we gotta ceate a new array to put the sorted one and, save the original array, which reminds me of the method called `Arrays.copyOf()`
So there we go.

2.Make sure we copy the original one to another array, just named it copyedOne, then we sort the array in the (). Then we compare them in sequence, make a counter record as soon as a pair not equal each other is found.

3.Return the counter, which is the answer we need to commit. This is it.

#### Code
```java
class Solution {
    public int heightChecker(int[] heights) {
        int[] copyOne = Arrays.copyOf(heights, heights.length);
        Arrays.sort(heights);

        int cnt = 0;
        for (int i = 0; i < heights.length; i++) {
            if (copyOne[i] != heights[i]) {
                cnt++;
            }
        }

        return cnt;
    }
}
```

