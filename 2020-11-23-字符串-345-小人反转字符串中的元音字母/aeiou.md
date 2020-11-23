#### Question [345. 反转字符串中的元音字母](https://leetcode-cn.com/problems/reverse-vowels-of-a-string/)

tag#字符串#



#### Description

```
编写一个函数，以字符串作为输入，反转该字符串中的元音字母。

 

示例 1：

输入："hello"
输出："holle"
示例 2：

输入："leetcode"
输出："leotcede"
 

提示：

元音字母不包含字母 "y" 。


```



#### Analysis

###### 1.小人的任务

将字符串中出现的元音识别然后将它们以相反的顺序插入到原来的位置. 

###### 2.小人怎么知道一个字符是不是元音字符?

写一个对单个字符匹配的方法, switch-case 匹配.

###### 3.小人如果走到了原因字符的位置, 怎么识别和记录?

识别可以用上面那个匹配的方法, 如果为正, 就说明当前字符是一个原因字符, 否则不是;

记录坐标和位置可以用容器, 因为后面还会走一趟, 第一趟只是记录元音字母的位置, 第二次是替换.

所以此处记录元音的位置只是为了后面从容器中提取"有还没没有". 所以可以用 Set.

> 不用 List 的原因在于 set 更直观. 

第一趟走完后, 小人就有一个容器, 容器里装有所有元音字符出现过的位置.

###### 4.然后呢?

然后就是第二次循环, 正式地制作字符串:

新建一个 `StringBuilder`.

由于上一步小人已经有了元音位置法宝. 所以第二次走的时候, 每次对当前的字符进行容器检验是否包含. 对了, 前面如果遇到有的话, 用一个栈收纳, 因为后面总是逆序"插入"的, 所以用栈的 pop 刚好. 这个栈是另一个纪录元音的容器. 等于说第一次实际上做了 2 个动作: 先是记录位置, 用于后边坐标检验, 后是收纳元音入栈.

如果检查当前坐标是上次经过记录元音出现过的位置, 就停下来, 从元音容器中放出一个, 那个刚好是上次最后一次加的元音, 追加到 `StringBuilder` 中.

如果当前坐标是其它字符的话, 就追加当前位置的字符.

###### 5.小人的两件法宝好厉害!



#### Code

```java
class Solution {
    //执行用时：10 ms, 在所有 Java 提交中击败了17.56%的用户
    public String reverseVowels(String s) {
        char[] chars = s.toCharArray();
        int len = chars.length;
        if (len <= 0)   return "";
        if (len == 1)   return s; 
        Stack<Character> aeiouStack = new Stack<>();
        //List<Integer> aeiouList = new ArrayList<>();  
       Set<Integer> container = new HashSet<>();
        //  字符数组的遍历
        for (int i = 0; i < len; i++) {
            char c = chars[i];
            if (isAEIOU(c)) {
                aeiouStack.push(c);
                container.add(i);     /*标记位置*/
            }
        }

        StringBuilder targetBuilder = new StringBuilder();

        for (int i = 0; i < len; i++) {
            char present = chars[i];
            if ( !aeiouStack.isEmpty() && container.contains(i) == true) {         /*检查位置记录*/                
                char aeious = aeiouStack.pop();
                targetBuilder.append(aeious);                
            }
            else {
                targetBuilder.append(present);                
            }                            
        }
        return targetBuilder.toString();
    }

    public boolean isAEIOU(char x) {
        boolean isAEIOU = false;
        switch(x) {
            case 'a':
            case 'e':
            case 'i':
            case 'o':
            case 'u':
            case 'A':
            case 'E':
            case 'I':
            case 'O':
            case 'U': isAEIOU = true;
            //default: isAEIOU = false;
        }
        return isAEIOU;
    }

}
```





#### 本期小人					

本期的小人总共做了 2 件事:

> 先是走第一趟字符串, 识别元音, 拿一个容器记录位置, 拿一个栈记录元音.
>
> 后是走第二趟字符串, 检验位置, 是否在手里的容器中, 是说明这个位置先前是一个元音字符, 就从栈的法宝中放出一个字符接上. 那个被放出来的刚好是新放进去的字符. 接上后就相当于反序.
>
> 如否则就正常接当前的字符.



