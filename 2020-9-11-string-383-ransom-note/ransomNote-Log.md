#### Question 赎金信问题 / [383. Ransom Note](https://leetcode-cn.com/problems/ransom-note/)



tag#string#



#### Description

```
给定一个赎金信 (ransom) 字符串和一个杂志(magazine)字符串，判断第一个字符串 ransom 能不能由第二个字符串 magazines 里面的字符构成。如果可以构成，返回 true ；否则返回 false。

(题目说明：为了不暴露赎金信字迹，要从杂志上搜索各个需要的字母，组成单词来表达意思。杂志字符串中的每个字符只能在赎金信字符串中使用一次。)

 

注意：

你可以假设两个字符串均只含有小写字母。

canConstruct("a", "b") -> false
canConstruct("aa", "ab") -> false
canConstruct("aa", "aab") -> true
```



#### Analysis

题意分析: 问字符串 a 能不能从 字符串 b 中找到组成 a 的所有字符 (a 中所有出现过的字符). 即问 a 是不是 b 的**子集**. (如果把字符串看成单个字符的集合的话).

解题分析: 

常规思路就是在 b 中按 a 的顺序寻找对应的字符是否存在, 能找到一个就剔除一个, 有一个没找到就说明不满足条件.

当然要做这题的话要以 a 为中心.

StringBuilder 有一个可以按位删除字符的方法 - `deleteCharAt(int index)`. 

可以通过 String 的类方法 `valueOf(char c)` 返回 c 的字符串形式, 再从 sbu 的里找到字符串对应的出现的位置. 然后再按位剔, 依次类推, 直到找到所有对应的字符(串), 并且都在 sbu 中剔除完毕了.



#### Code

```java
Class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        //	先对 b 字符串制造一个 sbu 对象, 后面完成字符的剔除
        StringBuilder sbu = new StringBuilder(magazine);	
        int index;
        for (char c : ransomNote.toCharArray()) {
            //	第一步: 找到 c 对应字符出现的位置            
            index = sbu.indexOf(String.valueOf(c));
            if (indexOf >= 0) {
                sbu.deleteCharAt(index);
            } else {
                return false;
            }            
        }
        return true;
    }
}
```







