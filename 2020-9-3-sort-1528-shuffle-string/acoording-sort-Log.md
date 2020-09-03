#### Question [1528. 重新排列字符串](https://leetcode-cn.com/problems/shuffle-string/)/[Shuffle String](https://leetcode-cn.com/problems/shuffle-string/)

tag#sort#



#### Description

```
给你一个字符串 s 和一个 长度相同 的整数数组 indices 。

请你重新排列字符串 s ，其中第 i 个字符需要移动到 indices[i] 指示的位置。

返回重新排列后的字符串。

 

示例 1：
```



```
输入：s = "codeleet", indices = [4,5,6,7,0,2,1,3]
输出："leetcode"
解释：如图所示，"codeleet" 重新排列后变为 "leetcode" 。
示例 2：

输入：s = "abc", indices = [0,1,2]
输出："abc"
解释：重新排列后，每个字符都还留在原来的位置上。
示例 3：

输入：s = "aiohn", indices = [3,1,4,2,0]
输出："nihao"
示例 4：

输入：s = "aaiougrt", indices = [4,0,2,6,7,3,1,5]
输出："arigatou"
示例 5：

输入：s = "art", indices = [1,0,2]
输出："rat"

提示：

s.length == indices.length == n
1 <= n <= 100
s 仅包含小写英文字母。
0 <= indices[i] < n
indices 的所有的值都是唯一的（也就是说，indices 是整数 0 到 n - 1 形成的一组排列）。
```



#### Analysis

题意分析: 重新排列字符串. 它会给到一个字符串, 和一个长度相等的整数数组. 整数数组中放的就是新的字符串每个字符对应的新位置. 也就是要按照整数数组中的顺序将字符串重新赋值. 把字符依次赋值到对应位置上, 即 indices 中规定的顺序. (虽然说题目给的图就十分清晰明了了)

解题分析:

字符串肯定不行, 第一印象觉得重新排序肯定不能用数组, 但是如果是按照一个标标准将一个数组重新赋值给另一个数组, 那就容易操作得多了.

#### Code

效果:

执行结果：

通过

显示详情

执行用时：2 ms, 在所有 Java 提交中击败了53.35%的用户

内存消耗：40 MB, 在所有 Java 提交中击败了29.16%的用户



```java
class Solution {
    public String restoreString(String s, int[] indices) {
        //  默认给定的整数数组是从 0 开始的
        char[] arr = new char[s.length()];
        int len = s.length();
        //  把当前位置的字符按照整数数组中值的位置赋值到新数组的对应位置中
        for (int i = 0; i < len; i++) {
            arr[indices[i]] = s.charAt(i);
        }
        return new String(arr);
    }
}
```







