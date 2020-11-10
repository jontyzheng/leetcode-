#### Question [1585. 检查字符串是否可以通过排序子字符串得到另一个字符串](https://leetcode-cn.com/problems/check-if-string-is-transformable-with-substring-sort-operations/)

tag##



#### Description

```
给你两个字符串 s 和 t ，请你通过若干次以下操作将字符串 s 转化成字符串 t ：

选择 s 中一个 非空 子字符串并将它包含的字符就地 升序 排序。
比方说，对下划线所示的子字符串进行操作可以由 "14234" 得到 "12344" 。

如果可以将字符串 s 变成 t ，返回 true 。否则，返回 false 。

一个 子字符串 定义为一个字符串中连续的若干字符。

 

示例 1：

输入：s = "84532", t = "34852"
输出：true
解释：你可以按以下操作将 s 转变为 t ：
"84532" （从下标 2 到下标 3）-> "84352"
"84352" （从下标 0 到下标 2） -> "34852"
示例 2：

输入：s = "34521", t = "23415"
输出：true
解释：你可以按以下操作将 s 转变为 t ：
"34521" -> "23451"
"23451" -> "23415"
示例 3：

输入：s = "12345", t = "12435"
输出：false
示例 4：

输入：s = "1", t = "2"
输出：false
 

提示：

s.length == t.length
1 <= s.length <= 105
s 和 t 都只包含数字字符，即 '0' 到 '9' 。
```



#### Analysis

题目的要求是给出两个字符串, 现在第一个序列有且只能通过子字符串的**升序**一种方式变化, 变成第二个序列. 且第二个序列的顺序是确定不变的.

1.易得, 如果第一个已经升序排列, 第二个也就是确定顺序的目标序列不是那个顺序的话, 按照题目的要求, 一定不能由第一个变换到第二个. 如示例 3.

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-11-09-string-1585-%E6%A3%80%E6%9F%A5%E5%AD%97%E7%AC%A6%E4%B8%B2%E6%98%AF%E5%90%A6%E5%8F%AF%E4%BB%A5%E9%80%9A%E8%BF%87%E6%8E%92%E5%BA%8F%E5%AD%90%E5%AD%97%E7%AC%A6%E4%B8%B2%E5%BE%97%E5%88%B0%E5%8F%A6%E4%B8%80%E4%B8%AA%E5%AD%97%E7%AC%A6/analysis-2.jpg" width="50%">

2.然后仔细分析一下为什么能通过子序列升序的序列可以通过升序变成另一个可以发现:

2.1.首先, 如果最后一位已经在第二个字符串的相同位置了, 就不需要再移动.

然后才依次看前面的字符看是否需要移动. 这说明判断顺序是**从后往前**的.

2.2.然后看移动的字符对照各自在 s 和 t 中的位置. 

可以看到, 总共有两种移动方向:

第一种, 一个字符要想将自己的顺序换到前面的位置, 比如说原先在 t 中是在倒数第二个, 现在要调到顺序第二个, 假设共有 5 个字符. ←.

变化方式只能通过升序, 那么要想跳到前面的位置, 那么它前面一定要有比它大的数, 这样, 它就能因为**升序**"被迫"调到前面.

根据评论区的提示, 序列的数组有且只有从 0 到 9 开始选. 也就是说前面的条件可以换成 (n, 9] 在 s 中的顺序排在 n 的前面. 即 position(number, 9) < position(n).

小结: 从后往前调, 大数在前面

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-11-09-string-1585-%E6%A3%80%E6%9F%A5%E5%AD%97%E7%AC%A6%E4%B8%B2%E6%98%AF%E5%90%A6%E5%8F%AF%E4%BB%A5%E9%80%9A%E8%BF%87%E6%8E%92%E5%BA%8F%E5%AD%90%E5%AD%97%E7%AC%A6%E4%B8%B2%E5%BE%97%E5%88%B0%E5%8F%A6%E4%B8%80%E4%B8%AA%E5%AD%97%E7%AC%A6/analysis-1.jpg" width="50%">

往后调的条件就是 0~9 中比它小的数排在它后面. position(0, number) > position(n). 如示例 2 中的 `8`.

小结: 从前往后调, 小数在后面.

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-11-09-string-1585-%E6%A3%80%E6%9F%A5%E5%AD%97%E7%AC%A6%E4%B8%B2%E6%98%AF%E5%90%A6%E5%8F%AF%E4%BB%A5%E9%80%9A%E8%BF%87%E6%8E%92%E5%BA%8F%E5%AD%90%E5%AD%97%E7%AC%A6%E4%B8%B2%E5%BE%97%E5%88%B0%E5%8F%A6%E4%B8%80%E4%B8%AA%E5%AD%97%E7%AC%A6/analysis-3.jpg" width="50%">



疑问: 问题就是题目的例子 3 中的 `5` 显示的好像不一样: 

应该从后往前调. 



#### Code





​			





