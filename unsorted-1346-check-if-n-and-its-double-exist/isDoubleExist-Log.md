#### Title: [检查整数及其两倍数是否存在](https://leetcode-cn.com/problems/check-if-n-and-its-double-exist/)/[Check If N and Its Double Exist](https://leetcode-cn.com/problems/check-if-n-and-its-double-exist/)



#### Description

```
给你一个整数数组 arr，请你检查是否存在两个整数 N 和 M，满足 N 是 M 的两倍（即，N = 2 * M）。

更正式地，检查是否存在两个下标 i 和 j 满足：

i != j
0 <= i, j < arr.length
arr[i] == 2 * arr[j]
 

示例 1：

输入：arr = [10,2,5,3]
输出：true
解释：N = 10 是 M = 5 的两倍，即 10 = 2 * 5 。
示例 2：

输入：arr = [7,1,14,11]
输出：true
解释：N = 14 是 M = 7 的两倍，即 14 = 2 * 7 。
示例 3：

输入：arr = [3,1,7,11]
输出：false
解释：在该情况下不存在 N 和 M 满足 N = 2 * M 。
 

提示：

2 <= arr.length <= 500
-10^3 <= arr[i] <= 10^3

```



#### Analysis

可以知道的是, 题目要找的数组中是否存在有两倍关系的数对.



受两数之和的启发, 首先想到 "用一个减去另一个, 拿差去匹配" 的思路.

这里的是找拿两倍积和一半去匹配.

是的, 这里需要 2 个匹配, 中间用 或 连接.



由提示得, 给定数组的长度至少会在 2 以上, 所以长度检验也免了.



#### Code

##### commit 1 

**94 / 104** 个通过测试用例

```java
class Solution {
    public boolean checkIfExist(int[] arr) {
        int first = arr[0];
        int target1 = 0;
        int target2 = 0;
        for (int i = 0; i < arr.length; i++) {
            target1 = 2*arr[i];
            target2 = arr[i]/2;
            for (int j = 0; j < arr.length; j++) {
                if (arr[j] == target1 || arr[j] == target2) {
                    return true;
                }
            }
        }
        return false;
    }
}
```





> 改: 二层循环里改 int j = i + 1

##### commit 2

**98 / 104** 个通过测试用例

```java
class Solution {
    public boolean checkIfExist(int[] arr) {        
        int target1 = 0;
        int target2 = 0;
        boolean isExist = false;
        for (int i = 0; i < arr.length; i++) {
            int first = arr[i];
            target1 = 2*arr[i];
            target2 = arr[i]/2;
            for (int j = i+1; j < arr.length; j++) {
                if (arr[j] == target1 || arr[j] == target2) {
                    isExist = true;
                }
            }
        }
        return isExist;
    }
}
```

> 显示未通过的测试用例:

```
输入：
[3,1,7,11]
输出：
true
预期：
false
```

> 分析: 其中的端倪就是, 当 3/2 的时候结果是 1, 结果遇到 1 的时候就会自动匹配, 造成返回错误的布尔值.
>
> 如何让 3/2 = 1.5
>
> - 修改将 `target` 修改成 double 类型.

#### 实验分析

事实证明:

在一个除法运算中, `int/int` 类型得到的也是 `int`类型的值. 结果用 `double` 盛装也没有. 得到的也是由可能被精度优化后的值(再拿去类型转换).

根据 Java 混合类型运算中, 低精度会向高精度上兼容, 自动向高精度的类型去靠.

这里的 被除数又不能修改了.

要想结果得到符合正常运算的结果, 拿 `3/2` 为例, 要想结果是 `1.5`, 再拿去到剩余部分循环匹配.

被除数是给定的整数数组, 已无法改变, 所以, 这时候应该让运算变成 "混合运算."

除以 `2.0`, 让运算自动变成混合运算. 这样, 算出来的商也是 1.5 了, 也不会出现误诊了.

#### Code

```java
class Solution {
    public boolean checkIfExist(int[] arr) {        
        int target1 = 0;
        double target2 = 0;        
        boolean isExist = false;
        for (int i = 0; i < arr.length; i++) {            
            target1 = 2*arr[i];
            target2 = arr[i]/2.0;       //  除数变 2 为 2.0
            for (int j = i+1; j < arr.length; j++) {
                if (arr[j] == target1 || arr[j] == target2) {
                    isExist = true;
                }
            }
        }
        return isExist;
    }
}
```

> 由于前一次 commit 中, 变量 `first` 并没有起到实际的作用, 所以可以省略.
>
> 可直接由 arr[i] 得到我们需要的 `target1` 和 `target2`

##### 效果

```
执行结果：通过	显示详情
执行用时：8 ms, 在所有 Java 提交中击败了5.25%的用户
内存消耗：39.4 MB, 在所有 Java 提交中击败了65.81%的用户
```

