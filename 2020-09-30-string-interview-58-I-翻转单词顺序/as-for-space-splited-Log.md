#### Question [剑指 Offer 58 - I. 翻转单词顺序](https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/)

tag#剑指 offer# #string#



#### Description

```
输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student. "，则输出"student. a am I"。

 

示例 1：

输入: "the sky is blue"
输出: "blue is sky the"
示例 2：

输入: "  hello world!  "
输出: "world! hello"
解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
示例 3：

输入: "a good   example"
输出: "example good a"
解释: 如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
 

说明：

无空格字符构成一个单词。
输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
如果两个单词间有多余的空格，将反转后单词间的空格减少到只含一个。
```



#### Analysis

由例子可得, 题目想要将字符串中各个字符串的顺序颠倒过来. 

```
输入: "the sky is blue"
输出: "blue is sky the"
```

这一点可以先将原字符串按照空格拆成各个字符串, 变成一个字符串数组后, 再**将数组从后往前遍历**然后追加实现.

第二个点就是最后的字符串前后不能由多余的空格.

> 如果是去掉单词空格的话, 可以用 `trim` 瘦身. 
>
> `trim` 可以掐头去尾.
>
> 然而, 由于这里字符串要求的最终结果头和尾都不能包含多余的空格. 所以可以提前掐掉字符串前后可能出现的空格.
>
> 再变数组.

第三个点就是想办法将数组中间多余的空格变成 1 个.

因为 `split` 只是按照特定字 (空格也算其中一个) 分离字符串: 如果是连续多个空格的话, 空格也会被当作一个数组项返回. 

这一点可以通过在追加的前面加上一个判定语句来消除, 如果是空格不追加上.

这样, 前面 `trim` 留下的空格组成的数组项也可以抵消掉了.



##### split 的例子

```java
/**
 * split(" ") 以一个空格分隔字符串
 * @author Jonty Zheng
 */

public class SplitTest2 {
    public static void main(String[] args) {
        String s = "a split   example";
        String[] res = s.split(" ");
        System.out.println();
        int i = 0;
        for (String ss:res) {
            System.out.println("第 " + i +  " 个字符串为:" + ss);
            i++;
        }
        System.out.println("第 2 个字符串的长度: " + res[2].length());      
        /*空格字符串的长度*/
    }
}

```

运行结果:

```
第 0 个字符串为:a
第 1 个字符串为:split
第 2 个字符串为:
第 3 个字符串为:
第 4 个字符串为:example
```

> 由最后一行可以看出, 所谓的空格字符串实际上也是长度为 0.
>
> 所以判定的条件是与("")匹配.



需要的注意就是, 因为是<u>每追加一个字符串, 接着追加一个空格</u>.

在最后记得将最后一次追加的空格给"掐"掉. 当然, 开头也需要. 针对第二个测试用例所示.





#### Code

```java
class Solution {
    public String reverseWords(String s) {
        //执行用时：1 ms, 在所有 Java 提交中击败了100.00%的用户
        //内存消耗：39.1 MB, 在所有 Java 提交中击败了30.20%的用户
        String str = s.trim();
        String[] strArr = str.split(" ");
        int len = strArr.length;
        
        StringBuilder resSbu = new StringBuilder();
        for (int i=len-1; i>=0; i--) {
            if (!strArr[i].equals("")) {        //  由 split 的例子可得
                String ss = strArr[i];  
                resSbu.append(ss).append(" ");
            }            
        }
        return resSbu.toString().trim();    	//  最后再去掉最后一个位置上的空格
    }
}
```





