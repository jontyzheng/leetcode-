#### Question [1189. “气球” 的最大数量](https://leetcode-cn.com/problems/maximum-number-of-balloons/)

tag##



#### Description

给你一个字符串 text，你需要使用 text 中的字母来拼凑尽可能多的单词 "balloon"（气球）。

字符串 text 中的每个字母最多只能被使用一次。请你返回最多可以拼凑出多少个单词 "balloon"。

 

示例 1：

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-11-30-%E5%AD%97%E7%AC%A6%E4%B8%B2-1189-balloon%E7%9A%84%E6%9C%80%E5%A4%A7%E6%95%B0%E9%87%8F/1536_ex1_upd.jpeg">

输入：text = "nlaebolko"
输出：1


示例 2：

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-11-30-%E5%AD%97%E7%AC%A6%E4%B8%B2-1189-balloon%E7%9A%84%E6%9C%80%E5%A4%A7%E6%95%B0%E9%87%8F/1536_ex2_upd.jpeg">

输入：text = "loonbalxballpoon"
输出：2


示例 3：

输入：text = "leetcode"
输出：0

提示：

1 <= text.length <= 10^4
text 全部由小写英文字母组成

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/maximum-number-of-balloons
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



------





#### Analysis

有 3 种理论上可行的方案

I. "两个容器"

将字符串当作一个容器, 把组成 balloon 所需要的字母当成一个容器. 比较包含, 每匹配一次计数几一次, 并将已经匹配的移除出去, 重复此操作.

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-11-30-%E5%AD%97%E7%AC%A6%E4%B8%B2-1189-balloon%E7%9A%84%E6%9C%80%E5%A4%A7%E6%95%B0%E9%87%8F/container-bottle.PNG" width="30%">

II. "最小公X数"

找出字符串种各个字母所拥有的数量, 取组成单位的最小数值.

III. 如果方案 II 是各个字母遍历一次字符串的话, 那么方案 III 就是它的简化版. 遍历一次找出各个字母的数量, 最后取最小.



#### Code

```java
class Solution {
    //执行用时：2 ms, 在所有 Java 提交中击败了80.48%的用户
	//内存消耗：36.9 MB, 在所有 Java 提交中击败了93.45%的用户
    public int maxNumberOfBalloons(String text) {
        int len = text.length();
        int numsOfA = 0;
        int numsOfB = 0;
        int numsOfL = 0;
        int numsOfO = 0;
        int numsOfN = 0;
        for (int i = 0; i < len; i++) {
            switch(text.charAt(i)) {
                case 'a':
                {
                    numsOfA++;
                    break;      /*加上 break 防止重复递增计数*/
                }
                case 'b':
                {
                    numsOfB++;
                    break;
                }
                case 'l':
                {
                    numsOfL++;
                    break;
                }
                case 'o':
                {
                    numsOfO++;
                    break;
                }
                case 'n':
                {
                    numsOfN++;
                    break;
                }
            }
        }
        return numsleast(numsOfA, numsOfB, numsOfN, numsOfL, numsOfO);
    }

    public int numsleast(int a, int b, int c, int d, int e) {
        /*增加下方两行排除 balon 计数的情况*/
        d = d == 1? 0:d;
        e = e == 1? 0:e;
        int[] ints = {a, b, c, d/2, e/2};
        Arrays.sort(ints);
        return ints[0];
    }
}
```





##### 测试用例过滤

```
输入：
"balon"
输出：
1
预期结果：
0
```

> 12/23

修改:

如果检验到 l 和 o 不满足一个的时候置为 0, 最后的 min 取最小.

```java
class Solution {
    public int maxNumberOfBalloons(String text) {
        int len = text.length();
        int numsOfA = 0;
        int numsOfB = 0;
        int numsOfL = 0;
        int numsOfO = 0;
        int numsOfN = 0;
        for (int i = 0; i < len; i++) {
            switch(text.charAt(i)) {
                case 'a':
                {
                    numsOfA++;
                    break;      /*加上 break 防止重复递增计数*/
                }
                case 'b':
                {
                    numsOfB++;
                    break;
                }
                case 'l':
                {
                    numsOfL++;
                    break;
                }
                case 'o':
                {
                    numsOfO++;
                    break;
                }
                case 'n':
                {
                    numsOfN++;
                    break;
                }
            }
        }
        return numsleast(numsOfA, numsOfB, numsOfN, numsOfL, numsOfO);
    }

    public int numsleast(int a, int b, int c, int d, int e) {
        /*增加下方两行排除 balon 计数的情况*/
        d = d == 1? 0:d;
        e = e == 1? 0:e;
        int[] ints = {a, b, c, d/2, e/2};
        Arrays.sort(ints);
        return ints[0];
    }
}
```







##### 历史方法记录

###### I: 两个集合

用一个集合类装字符串, 另一个装 `balloon`. 随着匹配计数后移除.

但由于集合类的 remove 方法会移除所有子集合中所含有的元素, 无法做到二次计数. 所以此方案行不通.

```java
import java.util.Collection;
class Solution {
    public int maxNumberOfBalloons(String text) {
        Collection<Character> container = makeupContainer(text);
        Collection<Character> bottle = makeupBottle();
        int count = 0;
        while (container.containsAll(bottle)) {
            count ++;
            for (char c : "balloon".toCharArray()) {
                container.remove(c);
            }                       
        }
        return count;
    }

    public Collection<Character> makeupContainer(String s) {
        Collection<Character> container = new ArrayList<>();        
        for (char c : s.toCharArray()) {
            container.add(c);
        }
        return container;
    }

    public Collection<Character> makeupBottle() {
        Collection<Character> bottle = new ArrayList<>();
        for (char c : "balloon".toCharArray()) {
            bottle.add(c);
        }
        return bottle;
    }
}
```

###### II. 取最小公X数

先计算各个字母的数量, 再取最小整数倍. 假设一个字符串 10^4  长. b a l o n 的统计时间加到一起就是 4 倍之多. 超出时间限制.

```java
class Solution {
    public int maxNumberOfBalloons(String text) {
        int numsOfB = countLetterNums(text, 'b');
        int numsOfA = countLetterNums(text, 'a');
        int numsOfL = countLetterNums(text, 'l')/2;
        int numsOfO = countLetterNums(text, 'o')/2;
        int numsOfN = countLetterNums(text, 'n');
        return Math.min(Math.min(Math.min(numsOfA, numsOfB), Math.min(numsOfL, numsOfO)), numsOfN);
    }

    public int countLetterNums(String s, char c) {
        String temp = s;
        int letterNum = 0;        
        char[] chars = s.toCharArray();        
        for (int i = 0; i < s.length(); i++) {
            while (s.charAt(i) == c)
                letterNum++;                    
        }
        return letterNum;
    }
}
```

###### III. 取最小数量集合

尝试能不能遍历一次就得出各个字母的数量——当然可以.

然后再写一个比较 5 个参数其中最小的数值的方法, 返回那个值就是需要答案了.

```java
class Solution {
    //执行用时：2 ms, 在所有 Java 提交中击败了80.48%的用户
	//内存消耗：36.9 MB, 在所有 Java 提交中击败了93.45%的用户
    public int maxNumberOfBalloons(String text) {
        int len = text.length();
        int numsOfA = 0;
        int numsOfB = 0;
        int numsOfL = 0;
        int numsOfO = 0;
        int numsOfN = 0;
        for (int i = 0; i < len; i++) {
            switch(text.charAt(i)) {
                case 'a':
                {
                    numsOfA++;
                    break;      /*加上 break 防止重复递增计数*/
                }
                case 'b':
                {
                    numsOfB++;
                    break;
                }
                case 'l':
                {
                    numsOfL++;
                    break;
                }
                case 'o':
                {
                    numsOfO++;
                    break;
                }
                case 'n':
                {
                    numsOfN++;
                    break;
                }
            }
        }
        return numsleast(numsOfA, numsOfB, numsOfN, numsOfL, numsOfO);
    }

    public int numsleast(int a, int b, int c, int d, int e) {
        /*增加下方两行排除 balon 计数的情况*/
        d = d == 1? 0:d;
        e = e == 1? 0:e;
        int[] ints = {a, b, c, d/2, e/2};
        Arrays.sort(ints);
        return ints[0];
    }
}
```





#### 本期心情						





