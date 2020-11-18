#### Question [804. 唯一摩尔斯密码词](https://leetcode-cn.com/problems/unique-morse-code-words/)

tag##



#### Description

```
国际摩尔斯密码定义一种标准编码方式，将每个字母对应于一个由一系列点和短线组成的字符串， 比如: "a" 对应 ".-", "b" 对应 "-...", "c" 对应 "-.-.", 等等。

为了方便，所有26个英文字母对应摩尔斯密码表如下：

[".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]
给定一个单词列表，每个单词可以写成每个字母对应摩尔斯密码的组合。例如，"cab" 可以写成 "-.-..--..."，(即 "-.-." + ".-" + "-..." 字符串的结合)。我们将这样一个连接过程称作单词翻译。

返回我们可以获得所有词不同单词翻译的数量。

例如:
输入: words = ["gin", "zen", "gig", "msg"]
输出: 2
解释: 
各单词翻译如下:
"gin" -> "--...-."
"zen" -> "--...-."
"gig" -> "--...--."
"msg" -> "--...--."

共有 2 种不同翻译, "--...-." 和 "--...--.".
 

注意:

单词列表words 的长度不会超过 100。
每个单词 words[i]的长度范围为 [1, 12]。
每个单词 words[i]只包含小写字母。


```



#### Analysis

##### 1.什么是摩尔斯密码词?

从题目中可知, 摩尔斯密码即是用 `.` `-` 组合表示 26 个字母, 然后人们再通过对照表去翻译成字符串, 转换成容易理解的单词(一个数组就是形成一个句子).

###### 对照表

<img src="" width="50%">



##### 2.题目要求的是什么?

"返回我们可以获得所有词不同单词翻译的数量"

为什么题目会说"可以从中识别出多少个不同的单词"? 从给出的例子结合"对照表", 翻译过来后, 我们可以看到毕竟所有组合有且仅有 `.` 和 `-` 组合而成, 多少都会有可能这个字母结尾的, 和后面字母开头拼接后, 刚好和另外一个虽然不是同一个单词, 但是同一个序列. 得到的重复序列, 就不计入最后数目.

<img src="" width="70%">

##### 3.怎么下手?

题目的思路可以很清晰:

1.将字母转换成字符, 再将字符拼接成字符串;

2.先后对比翻译后的序列, 只添加不重复的字符串.



###### 小心机

1.第 2 步可以直接使用 Java 集合类 `Set`, 它只会添加不重复的元素. 就像现实中真正的集合一样.

2.在一一匹配的时候写着写着忽然发现, 好像总是一上一下的 `-.-.-.-.` 一点一横的又容易出错, 干嘛不直接爪转成 0 和 1 的组合呢? 就像二进制一样, 也不影响最后的匹配.

于是, 代码结构就这么出现了.



#### Code

```java
class Solution {
    //执行用时：2 ms, 在所有 Java 提交中击败了99.09%的用户
    public int uniqueMorseRepresentations(String[] words) {
        int num = words.length;

        //Map<String, String> container = new HashMap<>();
        Set<String> container = new HashSet<>();
        for (int i = 0; i < num; i++) {
            String word = words[i];            
            int len = word.length();
            StringBuilder presentSbu = new StringBuilder();
            for (int k = 0; k < len; k++) {
                char c = words[i].charAt(k);
                String sub = selectChar(c);
                presentSbu.append(sub);
            }
            String presentStr = presentSbu.toString();
            //if (container.get(presentStr) == null)      
            //  container.put(presentStr, presentStr);            
            container.add(presentStr);
        }
        return container.size();
    }

    public String selectChar(char x) {
        String seq = "";
        switch(x) {
            case 'a':
            {
                seq = "01";
                break;
            }
            case 'b':
            {
                seq = "1000";
                break;
            }
            case 'c':
            {
                seq = "1010";
                break;
            }
            case 'd':
            {
                seq = "100";
                break;
            }
            case 'e':
            {
                seq = "0";
                break;
            }
            case 'f':
            {
                seq = "0010";
                break;
            }
            case 'g':
            {
                seq = "110";
                break;
            }
            case 'h':
            {
                seq = "0000";
                break;
            }
            case 'i':
            {
                seq = "00";
                break;
            }
            case 'j':
            {
                seq = "0111";
                break;
            }
            case 'k':
            {
                seq = "101";
                break;
            }
            case 'l':
            {
                seq = "0100";
                break;
            }
            case 'm':
            {
                seq = "11";
                break;
            }
            case 'n':
            {
                seq = "10";
                break;
            }
            case 'o':
            {
                seq = "111";
                break;
            }
            case 'p':
            {
                seq = "0110";
                break;
            }
            case 'q':
            {
                seq = "1101";
                break;
            }
            case 'r':
            {
                seq = "010";
                break;
            }
            case 's':
            {
                seq = "000";  //  o
                break;
            }
            case 't':
            {
                seq = "1";
                break;
            }
            case 'u':
            {
                seq = "001";
                break;
            }
            case 'v':
            {
                seq = "0001";
                break;
            }
            case 'w':
            {
                seq = "011";
                break;
            }
            case 'x':
            {
                seq = "1001";
                break;
            }
            case 'y':
            {
                seq = "1011";
                break;
            }
            case 'z':
            {
                seq = "1100";
                break;
            }
            //default: ;
        }
        return seq;
    }
}
```



​		



#### 本期心情						

没有想到最后的运行效果这么好.

但还是, 思路还是挺清晰的这道题.



