#### Question [443. 压缩字符串](https://leetcode-cn.com/problems/string-compression/)/[String Compression](https://leetcode-cn.com/problems/string-compression/)

tag#string#



#### Description

```
给定一组字符，使用原地算法将其压缩。

压缩后的长度必须始终小于或等于原数组长度。

数组的每个元素应该是长度为1 的字符（不是 int 整数类型）。

在完成原地修改输入数组后，返回数组的新长度。

 

进阶：
你能否仅使用O(1) 空间解决问题？

 

示例 1：

输入：
["a","a","b","b","c","c","c"]

输出：
返回 6 ，输入数组的前 6 个字符应该是：["a","2","b","2","c","3"]

说明：
"aa" 被 "a2" 替代。"bb" 被 "b2" 替代。"ccc" 被 "c3" 替代。
示例 2：

输入：
["a"]

输出：
返回 1 ，输入数组的前 1 个字符应该是：["a"]

解释：
没有任何字符串被替代。
示例 3：

输入：
["a","b","b","b","b","b","b","b","b","b","b","b","b"]

输出：
返回 4 ，输入数组的前4个字符应该是：["a","b","1","2"]。

解释：
由于字符 "a" 不重复，所以不会被压缩。"bbbbbbbbbbbb" 被 “b12” 替代。
注意每个数字在数组中都有它自己的位置。
 

提示：

所有字符都有一个ASCII值在[35, 126]区间内。
1 <= len(chars) <= 1000。

```



#### Analysis

题意分析: 按照 字符 + 字符出现次数的 "键值对" 压缩数组, 并返回压缩后数组的长度.

其中 不重复的字符没有 "值" 位.

如 ["a","b","b","b"], 压缩后的结果是 ["a","b","3"]。

另外, 一个位置只能放一个字符, 如果是超过一位数的数字位, 应才拆成十位和个位依次放在字母的后两位安放.

解题分析:

一开始我想的步骤是每遇到一个统计一个, 当重复的时候下一位 (原地修改后的数组) 放**数字**, 再重复就那该数组项加加. 不重复时下一位放**字母**. 而压缩的时候也要注意更新迭代变量. 

步骤较多, 在本小时内没有写完.

结果发现: 结果是返回一个整数, 也就是压不压缩没那么重要, 只要能统计出压缩后数组后的长度即可.



#### Code

评论区某答案

```java
class Solution {
     public int compress(char[] chars) {
        int n = chars.length, cur = 0;
        for (int i = 0, j = 0; i < n; i = j) {
            while (j < n && chars[j] == chars[i]) j++;
            chars[cur++] = chars[i];
            if (j - i == 1) continue;
            for (char c : String.valueOf(j - i).toCharArray()) chars[cur++] = c;
        }
        return cur;
    }
}
```



commit 1

```java
class Solution {
    public int compress(char[] chars) {
        //  1. 没有下一个不加数字
        //  当计数后, 与 10 比较, 并判断是否需要下一位放计数值的个位 下一位放 count/10 这一位上放
        //  压缩更新迭代器
        int len = chars.length;
        if (len == 1) {
            return 1;
        }
        //  [34, 126] 常见符号, 数字, 字母
        //  第一位总是不变的        
        //  与前一位判断决定"压缩位的下一位"放的是字母(不变)还是数字位(数字位数值加加)
        //  不一定要得到"目标数组" (压缩数组) 只要统计数量返回
        int i = 1;
        while (i < len) {
            if (char)
        }

    }
}
```









