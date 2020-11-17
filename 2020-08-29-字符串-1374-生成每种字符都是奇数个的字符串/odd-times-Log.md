#### Question [1374. 生成每种字符都是奇数个的字符串](https://leetcode-cn.com/problems/generate-a-string-with-characters-that-have-odd-counts/)/[Generate a String With Characters That Have Odd Counts](https://leetcode-cn.com/problems/generate-a-string-with-characters-that-have-odd-counts/)

tag#string#



#### Description

```
给你一个整数 n，请你返回一个含 n 个字符的字符串，其中每种字符在该字符串中都恰好出现 奇数次 。

返回的字符串必须只含小写英文字母。如果存在多个满足题目要求的字符串，则返回其中任意一个即可。

 

示例 1：

输入：n = 4
输出："pppz"
解释："pppz" 是一个满足题目要求的字符串，因为 'p' 出现 3 次，且 'z' 出现 1 次。当然，还有很多其他字符串也满足题目要求，比如："ohhh" 和 "love"。
示例 2：

输入：n = 2
输出："xy"
解释："xy" 是一个满足题目要求的字符串，因为 'x' 和 'y' 各出现 1 次。当然，还有很多其他字符串也满足题目要求，比如："ag" 和 "ur"。
示例 3：

输入：n = 7
输出："holasss"
```





#### Analysis

题意分析:

这道题实际上是给你一个整数 `n`, 要求返回 `n` 个符合条件的小写字母.

这个条件就是字符都只出现奇数次, 不能是偶数次的. 所以不能有 `aabb` 这样的情况. 要像 `pppz`, `xy`, `holasss` 这样的情况.

发现没有, 题目并没有给出一定要从由那些字母组成, 只要返回这么一个符合条件的字符串即可.

那么机会来了, 一个字母肯定不行, 那就 `a` 和 `b`, 由 `a` 和 `b` 组成的字符串就可以组成所有题目要求的字符串了.

组成的序列如下:

1. 给定整数为奇数, 那返回奇数个 `a` 就好了.
2. 给定整数为偶数, 那返回 "一半加一个 `a`, 一半减一个 `b` " 就可以了.

然而这里在第 2 种情况中又有个奇妙的点出现了: 

同样的偶数, 却有不同的情况:

- 2 = 1+1
- 4= 2+2
- 6=3+3
- 8=4+4

如果按照 `0 < n/2-1` 追加 `a`, `0 < n/2+1` 追加 `b`

```java
//  如果为偶数个的情况
        else {
            for (int i = 0; i < n/2-1; i++) {
                builder.append('a');
            }
            for (int i = 0; i < n/2+1; i++) {
                builder.append('b');
            }
        }
```

当 `n` 为 2 的时候,  `n/2-1` 得到的是 0, `a` 没追加成功, `n/2+1` 得到的是 2, 这时追加到的说就是 2 个 `b`.

而这并不是 `n` 因为在开始 1, 2, 3 这种小范围内而出现的情况.

当 `n` 为 6 的时候, 这是, 前者得到 2, 后者得到 4, 这时候就事与愿违了.

由于奇数次的情况我们可以保证符合情况, 那我们可以列出从 2 到后面几位的偶数, 看看它们的要求的情况:

```
2=1+1

4=1+3

6=3+3

8=4+4 (从这里开始就改成按照偶数的一半枚举)

10=5+5

12=6+6

14=7+7

16=8+8

...
```



这个时候就出现答案了: 有些偶数天生就是由两个奇数组成的, 有的是由两个偶数组成的. 而恰好的是, 这个数字都是一个隔一个出现的. 如 `10` 是由两个 `5` 组成, `12` 刚好是由两个 `6` 组成的, `14` 是由两个 `7` 组成, `16` 刚好又是 `8` 的两倍.

所以再将这两种情况细分出来. (以下 "目标" 为目标整数的一半)

1. 当目标为奇数的时候, 按 (一半, 一半) 先后追加 `a` 和 `b`;
2. 当目标为偶数的时候, 按 (一半-1, 一半+1) 先后追加  `a` 和 `b`.

具体实现如下.

#### Code

```java
class Solution {
    public String generateTheString(int n) {
        StringBuilder builder = new StringBuilder();        
        if (n%2 != 0) {
            for (int i = 0; i < n; i++) {
                builder.append('a');
            }
        }
        //  如果 n 为偶数
        else {
            //  拿到 n 的一半设为 half
            int half = n/2;
            //  如果 half 本身是奇数, 如 6 = 3+3, 就按照(一半, 一半)追加a, b
            if (half%2 != 0) {
                for (int i = 0; i < n/2; i++) {
                    builder.append('a');
                }
                for (int i = 0; i < n/2; i++) {
                    builder.append('b');
                }
            }
            //  如果 half 本身是偶数, 如 4 = 2+2, 就按照(一半-1, 一半+1)追加a, b
            else if (half%2 == 0){
                for (int i = 0; i < n/2-1; i++) {
                    builder.append('a');
                }
                for (int i = 0; i < n/2+1; i++) {
                    builder.append('b');
                }
            }
        }  
        return builder.toString();
    }
}
```

执行结果:

```
输入
4
输出
"abbb"
预期结果
"pppz"
```

执行效果:

```
执行结果：
通过
显示详情
执行用时：1 ms, 在所有 Java 提交中击败了98.77%的用户
内存消耗：37.1 MB, 在所有 Java 提交中击败了54.01%的用户
```





