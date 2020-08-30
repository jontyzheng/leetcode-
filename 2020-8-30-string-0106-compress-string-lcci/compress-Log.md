#### Question [面试题 01.06. 字符串压缩](https://leetcode-cn.com/problems/compress-string-lcci/)/[Compress String LCCI](https://leetcode-cn.com/problems/compress-string-lcci/)

tag#string#



#### Description

```
字符串压缩。利用字符重复出现的次数，编写一种方法，实现基本的字符串压缩功能。比如，字符串aabcccccaaa会变为a2b1c5a3。若“压缩”后的字符串没有变短，则返回原先的字符串。你可以假设字符串中只包含大小写英文字母（a至z）。

示例1:

 输入："aabcccccaaa"
 输出："a2b1c5a3"
示例2:

 输入："abbccd"
 输出："abbccd"
 解释："abbccd"压缩后为"a1b2c2d1"，比原字符串长度更长。
提示：

字符串长度在[0, 50000]范围内。
```





#### Analysis

题意分析:

1.已知给定字符串只有字母组成, 现要求将原字符串变成 "字母+字母连续次数" 的字符串.

2.只有当变化后的字符串的长度小于原字符串的时候才输出改装后的字符串.

解题分析:

第一步中的连续次数用下一个位置的字符比较进行判断, 计时器用 `StringBuilder` 的追加.

由于整个字符串最后总是一个字符+一个数字的形式**且**数字至少为 1.

所以追加玩当前位置字符后再追加上计数器即可. 随后更新迭代器后.

第二步中的选择性返回用流程控制中的 `?:`

#### Code

效果:

```
执行结果：
通过
显示详情
执行用时：7 ms, 在所有 Java 提交中击败了37.47%的用户
内存消耗：40 MB, 在所有 Java 提交中击败了27.94%的用户
```



code:

```java
class Solution {
    public String compressString(String S) {
        int len = S.length();
        StringBuilder builder = new StringBuilder();
        
        for (int i  = 0; i < len; i++) {
            int count = 1;      //  update 1: 局部计时器
            builder.append(S.charAt(i));    //  update 2: 优先追加默认的当前字母
            int j = i + 1;
            while (j < len && S.charAt(i) == S.charAt(j)) {
                count++;      //    count 加的是邻近相等
                j++;          //    j 加的是节点往右走
            }            
            //if (count != 1)   
            i += count - 1;     //    update 3: 遇到重复项后更新下一个迭代器                   
                                //  i += count - 1 的原因因为是 for 执行完循环体就是迭代器的更新       
            builder.append(count);
        }
        String another = builder.toString();
        return another.length() < S.length()? another : S;        
    }
}
```



提交历史:

commit 1

> 效果是
>
> ```
> 18 / 32 个通过测试用例
> 状态：解答错误
> 提交时间：几秒前
> 输入：
> "aabcccccaa"
> 输出：
> "aabcccccaa"
> 预期：
> "a2b1c5a2"
> ```
>
> `count` 初始值应该设为 1 而不是 0.
>
> 至少都是为 1 嘛, 追加字母后追加数字 1 的.

```java
class Solution {
    public String compressString(String S) {
        int len = S.length();
        StringBuilder builder = new StringBuilder();
        
        for (int i  = 0; i < len; i++) {
            int count = 0;      //  局部计时器
            for (int j = i; j < len && S.charAt(i) == S.charAt(j); j++) {
                count++;
            }
            builder.append(S.charAt(i));
            builder.append(count);
        }
        String another = builder.toString();
        //return S : another? S.length() > another.length();
        if (another.length() < S.length())
            return another;
        return S;
    }
}
```



commit 2

> 

```java
class Solution {
    public String compressString(String S) {
        int len = S.length();
        StringBuilder builder = new StringBuilder();
        
        for (int i  = 0; i < len; i++) {
            int count = 1;      //  update 1: 局部计时器
            builder.append(S.charAt(i));    //  update 2: 优先追加默认的当前字母
            for (int j = i; j < len; j++) {
                if (S.charAt(j) == S.charAt(i)) //  当邻近的后续结点相等时计数器加加再追加
                    count++;                
            }            
            builder.append(count);
        }
        String another = builder.toString();
        return another.length() < S.length()? another : S;        
    }
}
```



commit 3

```java
class Solution {
    public String compressString(String S) {
        int len = S.length();
        StringBuilder builder = new StringBuilder();
        
        for (int i  = 0; i < len; i++) {
            int count = 1;      //  update 1: 局部计时器
            builder.append(S.charAt(i));    //  update 2: 优先追加默认的当前字母
            for (int j = i; j < len; j++) {
                if (S.charAt(j) == S.charAt(i)) //  当邻近的后续结点相等时计数器加加再追加
                    count++;                
            }            
            builder.append(count);
        }
        String another = builder.toString();
        return another.length() < S.length()? another : S;        
    }
}
```

测试用例分析:

```
输入：
"aabcccccaa"
输出：
"aabcccccaa"
预期：
"a2b1c5a2"
```

> 由于输出的结果还是原来的字符, 所以我想是因为 builder 后的字符串实际长度还超过了原来的字符串.
>
> 经过一些调试, 出现了输出为类似 `a3c5a2` 形式的作用, 说明 builder 是由起到作用的.
>
> 然后却缺少了 `b2`
>
> 经过检查遍历节点的重复, 成功找出了 "字符串超过原字符串" 以及 "缺少其中部分字符" 的原因所在
>
> 迭代的节点:
>
> 1.当追加完当前的字母后应该根据 `count` 的值**跳**迭代器 `i`, 否则会出现像 `a3a4..` 这样的重复字母追加.
>
> 2.迭代器的更新为 `i += count - 1`, 因为这部分执行完后 `i` 总会加 1.





