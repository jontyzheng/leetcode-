#### Question [反转字符串中的单词 III](https://leetcode-cn.com/problems/reverse-words-in-a-string-iii/)/[Reverse Words in a String III](https://leetcode-cn.com/problems/reverse-words-in-a-string-iii/)

tag#String#



#### Description

```
给定一个字符串，你需要反转字符串中每个单词的字符顺序，同时仍保留空格和单词的初始顺序。

 

示例：

输入："Let's take LeetCode contest"
输出："s'teL ekat edoCteeL tsetnoc"
 

提示：

在字符串中，每个单词由单个空格分隔，并且字符串中不会有任何额外的空格。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/reverse-words-in-a-string-iii
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```





#### Analysis

题意分析: 字符串是一个带空格开分的字符串. 现在要将其中各个"子部分"倒置, 而不是整个字符串中的字符从头到尾倒置. 原来整体的顺序没有变.





分析: 

是将给定的字符串首先按照空格给它分开, 变成一个字符串数组.  因为一整个字符串肯定倒置还保证其中各个空格隔开的部分顺序还不变对吧, 它是一个整体. 按空格分开拆成一个字符串数组. 再对其中项 (小字符串) 进行倒置.

最后换上另一个字符串, 追加倒置后的数组项, 每追加一个添加多一个空格.





#### 评论区优秀答案

```java
class Solution {
    public String reverseWords(String s) {
        if (s == null || s.length() == 0) {
            return s;
        }
        String[] strs = s.split(" ");
        StringBuilder sb = new StringBuilder();
        for (String str : strs) {
            sb.append(new StringBuilder(str).reverse() + " ");
        } 
        return sb.toString().trim();
    }
}
```

效果:

```
执行结果：通过
显示详情
执行用时：6 ms, 在所有 Java 提交中击败了75.38%的用户
内存消耗：40.6 MB, 在所有 Java 提交中击败了30.07%的用户
```



#### Code

但是我自己写的在有限的时间内还没 ac, 

##### commit 1

```java
class Solution {
    public String reverseWords(String s) {
        String[] strArr = s.split(" ");    //  {"Let's", "take", "LeetCode", "contest"}
        
        //  倒置: 在一个字符串数组里将各个小字符串倒置
        for (int i = 0; i < strArr.length; i++) {
            int len = strArr[i].length();
            for (int j = 0; j < len; j++) {  //  "Let's"
                //  中间值交换法
                char temp = ' ';
                int m = len - j - 1;         //  镜面位  -j+1
                temp = strArr[i].charAt(m);          
                strArr[i].charAt(m) = strArr[i].charAt(j);   	//	编译错误           
                strArr[i].charAt(j) = temp;               
            }
        }
        //  追加: 将字符串数组中的字符依次加入到另一个字符串中, 每次加上一个补一个空格符
        StringBuilder sbu = new StringBuilder();    //  此处使用 sbu 方便 append 上空格
        for (int i = 0; i < strArr.length; i++) {
            int len = strArr[i].length();
            for (int j = 0; j < len; j++) {
                //  逐个追加法
                sbu.append(strArr[i].charAt(j));
                if (j == len - 1) 
                    break;
            }
            sbu.append(' ');
        }
        return sbu.toString();
    }
}
```



由于 charAt(int index) 无法用于直接赋值替换, 所以用先转字符数组再赋值的方法, 然后再换回去数字符串



##### commit 2

先将当前的字符串转字符数组, 再对字符数组进行倒置, 最后将字符数组转字符串赋值给当前字符串.

所用到的方法:

1. +toCharArray(): char[]
2. +copyValueOf(char[] data): String

```java
class Solution {
    public String reverseWords(String s) {
        String[] strArr = s.split(" ");    //  {"Let's", "take", "LeetCode", "contest"}
        
        //  倒置: 在一个字符串数组里将各个小字符串倒置
        for (int i = 0; i < strArr.length; i++) {            
            char[] charStr = strArr[i].toCharArray();
            int len = charStr.length;
            for (int j = 0; j < len; j++) {  //  "Let's"
                //  中间值交换法
                char temp;
                int mirror = len - j - 1;         //  镜面位  -j+1
                temp = charStr[mirror];          
                charStr[mirror] = charStr[j];
                charStr[j] = temp;            
            }
            strArr[i] = String.copyValueOf(charStr);
        }
        //  追加: 将字符串数组中的字符依次加入到另一个字符串中, 每次加上一个补一个空格符
        StringBuilder sbu = new StringBuilder();    //  此处使用 sbu 方便 append 上空格
        for (int i = 0; i < strArr.length; i++) {
            int len = strArr[i].length();
            for (int j = 0; j < len; j++) {
                //  逐个追加法
                sbu.append(strArr[i].charAt(j));
                if (j == len - 1) 
                    break;
            }
            sbu.append(' ');
        }
        return sbu.toString();
    }
}
```

结果

```
执行结果：
解答错误
显示详情
输入：
"Let's take LeetCode contest"
输出：
"Let's take LeetCode contest "
预期结果：
"s'teL ekat edoCteeL tsetnoc"
```

时间有限, 还是没有找出出错的地方.

.
