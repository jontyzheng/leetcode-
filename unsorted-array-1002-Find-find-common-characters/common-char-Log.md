#### Question: [查找常用字符](https://leetcode-cn.com/problems/find-common-characters/)



#### Description

```
给定仅有小写字母组成的字符串数组 A，返回列表中的每个字符串中都显示的全部字符（包括重复字符）组成的列表。例如，如果一个字符在每个字符串中出现 3 次，但不是 4 次，则需要在最终答案中包含该字符 3 次。

你可以按任意顺序返回答案。

 

示例 1：

输入：["bella","label","roller"]
输出：["e","l","l"]
示例 2：

输入：["cool","lock","cook"]
输出：["c","o"]
 

提示：

1 <= A.length <= 100
1 <= A[i].length <= 100
A[i][j] 是小写字母
```



#### Analysis

题目讲的在给定一个字符串数组中, 找到各个字符串中出现字符的交集.

重复也要找出来.

因为提示中有说

> `A[i][j]` 是小写字母

所以我想的是将这个字符串数组转换成二维的字符数组.

然后, 找出其中长度最长的作为循环.

按照二维数组的方法, 集体遍历, 依次找出其中的数字., 也就是 ASCII 码值比较嘛. [96-122] 的区间.

每找到一个共有的随即拿一个计数器一次记录. 这个计数器作为一个新建数组的标准, 也是最后返回的原型数组.

新建一个长度为前面计数器数值的 int 类型数组.

将内部的元素转化为对应的字符.



#### Code

时间有限, 所以还没来得及实现, 下面是评论区里的答案.

```java
class Solution {
    public List<String> commonChars(String[] A) {
        List<String> list = new ArrayList<>();
        int[] res = new int[26];
        for (char c : A[0].toCharArray()) {
            res[c - 'a']++;
        }
        for (int i = 1; i < A.length; i++) {
            int[] temp = new int[26];
            for (char c : A[i].toCharArray()) {
                temp[c - 'a']++;
            }
            for (int j = 0; j < 26; j++) {
                res[j] = Math.min(res[j], temp[j]);
            }
        }
        for (int i = 0; i < res.length; i++) {
            if (res[i] > 0) {
                for (int j = 0; j < res[i]; j++) {
                    list.add(((char) ('a' + i) + ""));
                }
            }
        }
        return list;
    }
}
```



 

