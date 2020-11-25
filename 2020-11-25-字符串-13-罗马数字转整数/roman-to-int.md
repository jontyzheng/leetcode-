#### Question [13. 罗马数字转整数](https://leetcode-cn.com/problems/roman-to-integer/)

tag##



#### Description

```
罗马数字包含以下七种字符: I， V， X， L，C，D 和 M。

字符          数值
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
例如， 罗马数字 2 写做 II ，即为两个并列的 1。12 写做 XII ，即为 X + II 。 27 写做  XXVII, 即为 XX + V + II 。

通常情况下，罗马数字中小的数字在大的数字的右边。但也存在特例，例如 4 不写做 IIII，而是 IV。数字 1 在数字 5 的左边，所表示的数等于大数 5 减小数 1 得到的数值 4 。同样地，数字 9 表示为 IX。这个特殊的规则只适用于以下六种情况：

I 可以放在 V (5) 和 X (10) 的左边，来表示 4 和 9。
X 可以放在 L (50) 和 C (100) 的左边，来表示 40 和 90。 
C 可以放在 D (500) 和 M (1000) 的左边，来表示 400 和 900。
给定一个罗马数字，将其转换成整数。输入确保在 1 到 3999 的范围内。

 

示例 1:

输入: "III"
输出: 3
示例 2:

输入: "IV"
输出: 4
示例 3:

输入: "IX"
输出: 9
示例 4:

输入: "LVIII"
输出: 58
解释: L = 50, V= 5, III = 3.
示例 5:

输入: "MCMXCIV"
输出: 1994
解释: M = 1000, CM = 900, XC = 90, IV = 4.
 

提示：

题目所给测试用例皆符合罗马数字书写规则，不会出现跨位等情况。
IC 和 IM 这样的例子并不符合题目要求，49 应该写作 XLIX，999 应该写作 CMXCIX 。
关于罗马数字的详尽书写规则，可以参考 罗马数字 - Mathematics 。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/roman-to-integer
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```





#### Analysis

##### 1.罗马数字是什么? 它有什么组成规则?

罗马数字就是平时看到的类似版本号 V, IV 这一类数字的表示方法.

它的规则很简单:

除了基本的 I(1) V(5) X(10) L(50) C(100) D(500) M(1000) 都是按照值一路相加, 除非, 相邻两个之间组合一下的这些组合

```
IV 4
IX 9
VX 40
XC 90
CD 400
CM 900
```

这些都是要么和 4 有关, 要么和 9 有关.

只有遇到这些的时候才是换成它们两两组合对应的数值累加.

##### 2.如何可以判断程序怎么识别它们呢?

首先, 我们得自己先熟悉罗马数字的基本数字.

比如任意给出一个罗马数字, 按照规则把它们转换成对应的数字. 

> eg: 49 = 40 + 9 = XC + IX
>
> eg: 999 = 900 + 90 + 9 = CM + XC + IX
>
> eg: 302 = 300 + 2 = CCCII
>
> eg: 404 = 400 + 4 = CD + IV

反过来的时候呢? 

> eg: MCMXCIV

当自己写的时候, 就会发现, 自己是从右边往左边开始找有没有特殊组合的.

这时候就是一个启发了, 小人应该从右往左走, 一路判断:

如果, 连接前面一个字符匹配到一个"特殊组合"的时候, 就换算成组合的值;

如果, 临时组合不是特殊的话, 说明是像"VIII"一类的情况, 那就一一换算累加.

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-11-25-%E5%AD%97%E7%AC%A6%E4%B8%B2-13-%E7%BD%97%E9%A9%AC%E6%95%B0%E5%AD%97%E8%BD%AC%E6%95%B4%E6%95%B0/convert-normal.PNG" width="70%">

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-11-25-%E5%AD%97%E7%AC%A6%E4%B8%B2-13-%E7%BD%97%E9%A9%AC%E6%95%B0%E5%AD%97%E8%BD%AC%E6%95%B4%E6%95%B0/convert-more.PNG" width="70%">

##### 3.听起来很复杂, 有没有比较简单的流程图呢?

有的

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-11-25-%E5%AD%97%E7%AC%A6%E4%B8%B2-13-%E7%BD%97%E9%A9%AC%E6%95%B0%E5%AD%97%E8%BD%AC%E6%95%B4%E6%95%B0/process.PNG" width="70%">

##### 4.从字符(串)到数值的转换一定要用到匹配方法的? 有没有什么数据结构呢?

I V .. 单个字符的匹配可以用 map - Map<Character, Integer>;

IV, IX.. 组合字符的匹配可以用map - Map<String, Integer>;

一开始我用的是专门拿一个map做"字符组合-面值"提取, 拿一个map做"字符-字符"组合匹配的. 但是后面本来 6 对的组合出来长度是 3 才发现, I-V 和 I-X 的 key 重复了, map 默认是 key 唯一的. 

后来就改成"拿字符值匹配返回结果"的思路, 就写成换成"字符组合-面值"的 map(makeupMap), 发现了既可以用来判断临时组合是否字符组合, 又可以取值. 省了一个 map(valueMap). 

当然, 还有一个"字符-面值"的单元 map(unitMap)



#### Code

```java
class Solution {
    //执行用时：12 ms, 在所有 Java 提交中击败了10.00%的用户
    public int romanToInt(String s) {                
        char[] chars = s.toCharArray();
        int len = chars.length;
        Map<Character, Integer> groupMap = makeupMap();        
        //Map<String, Integer> valueMap = valueMap();   /*改装组合检验 map 后用 get(key) */
        Map<Character, Integer> unitMap = unitMap();
        int sum = 0;
        for (int i = len - 1; i >= 0; i--) {
            char present = chars[i];

            if (i != 0) {        /*update log: 修改成 >= 0*/        
                char former = chars[i-1];
                StringBuilder builder = new StringBuilder();
                builder.append(former).append(present);         /*update log: 先放 former, 再放 present*/
                String tempGourp = builder.toString();
                if (groupMap.containsKey(tempGourp) == true) {  /*update log: 改成 containsKey 判断*/
                    int groupValue = groupMap.get(tempGourp);   /*update log: 这里应该改成从 group 中取值*/
                    sum += groupValue;
                    i--;
                }
                else {
                    int value = unitMap.get(present);
                    sum += value;
                }
            }
            else {
                int value = unitMap.get(present);
                sum += value;
            }
        }
        return sum;
    }    

    /*组合map update log: 把 I-V 改成 "IV"-4 的 map*/
    public Map makeupMap() {
        Map<String, Integer> map = new HashMap<>();
        map.put("IV", 4);  //  4
        map.put("IX", 9);  //  9
        map.put("XL", 40);  //  40
        map.put("XC", 90);  //  90
        map.put("CD", 400);  //  400
        map.put("CM", 900);  //  900
        return map;
    }

    /*面值map*/
    public Map valueMap() {
        Map<String, Integer> map = new HashMap<>();
        map.put("IV", 4);
        map.put("IX", 9);
        map.put("XL", 40);
        map.put("XC", 90);
        map.put("CD", 400);
        map.put("CM", 900);        
        return map;
    }

    /*单位map*/
    public Map unitMap() {
        Map<Character, Integer> map = new HashMap<>();
        map.put('I', 1);
        map.put('V', 5);
        map.put('X', 10);
        map.put('L', 50);
        map.put('C', 100);
        map.put('D', 500);
        map.put('M', 1000);
        return map;
    }
}
```





#### 本期心情						

字符转成数字, 刚看到的时候就有种好像之前做过的"摩尔密码转换".

过程框架都是类似的, 另外开一个方法字面值匹配. 只是这一个有一点需要比较细.

> 小人走的时候:
>
> 因为如果是第一位的时, 没有前一个字符, 组成临时组合, 所以它要单独来看.
>
> 到了 i == 0 的时候一定是累加当前字符的字符的对应数值了
>
> 如果它没有被后面的字符**合并**过去的话. 每遇到一次组合累加上一次组合值之后前面那个都不需要重复判断了, 记得 i--.



##### 测试用例pk

