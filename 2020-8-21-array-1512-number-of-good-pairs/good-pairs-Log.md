#### Question [好数对的数目](https://leetcode-cn.com/problems/number-of-good-pairs/)/[Number of Good Pairs](https://leetcode-cn.com/problems/number-of-good-pairs/)

tag#array#



#### Description

```
给你一个整数数组 nums 。

如果一组数字 (i,j) 满足 nums[i] == nums[j] 且 i < j ，就可以认为这是一组 好数对 。

返回好数对的数目。

 

示例 1：

输入：nums = [1,2,3,1,1,3]
输出：4
解释：有 4 组好数对，分别是 (0,3), (0,4), (3,4), (2,5) ，下标从 0 开始
示例 2：

输入：nums = [1,1,1,1]
输出：6
解释：数组中的每组数字都是好数对
示例 3：

输入：nums = [1,2,3]
输出：0
 

提示：

1 <= nums.length <= 100
1 <= nums[i] <= 100

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/number-of-good-pairs
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```



#### Analysis

依题意得, 存在相等的一对数组元素就算一个好数对.

需要注意的是, 每 3 个元素在一起可以有 3 个这样的好数对; 每 4 个在一起在可以有 6 个这样的好数组. 找到相等的元素数后计算 C<sub>n</sub><sup>2</sup> 的值得到.



需要注意的点是:

1. 由于计数器从 0 开始, 每多找到一个匹配相等的项时得到的组合数其实是 C<sup>2</sup><sub>count+1</sub>. 

   如计数器初始值为 0, 没找到一个就是在 2 个元素中找这样的数组对.

2. 如果从头到尾匹配相等的话, 有可能会重复匹配. 由于 `提示` 中标明了 `1 <= nums[i] <= 100`. 此时将匹配后的数组元素置为 `0`, 且加入到条件判断的条件中可以避免这一情况的发生.



#### Code

#### commit 1

```java
class Solution {
    public int numIdenticalPairs(int[] nums) {
          
        int pairs = 0; 
        for (int i = 0; i < nums.length; i++) {
            int count = 0;
            for (int j = i+1; j < nums.length; j++) {                
                if (nums[j] == nums[i] && nums[j] != 0) {
                    count++;
                    nums[j] = 0;
                }                
            }            
            pairs += (count+1)*count/2;
        }
        return pairs;
    }
}
```

效果:

```
执行结果：通过
显示详情
执行用时：2 ms, 在所有 Java 提交中击败了6.07%的用户
内存消耗：37.3 MB, 在所有 Java 提交中击败了20.32%的用户
```







