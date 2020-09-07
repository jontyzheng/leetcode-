#### Question

tag##



#### Description [1436. 旅行终点站](https://leetcode-cn.com/problems/destination-city/)/[Destination City](https://leetcode-cn.com/problems/destination-city/)



#### Analysis

题意分析: 给出一个 [起点, 终点] 组成的一个长列表. 其中各个对相互衔接, 即总有一条路线的终点是通往另外一个目的的起点. 只有目的地例外.

解题分析: 由题意分析, 也就是找出唯一一个没有在起点位置上出现过的第二项. (终点项)

物理意义: 找出一个唯一一个没有被当作成起点位置的终点, 它就是最终目的地.

方法: 由于其它的第二项, 总能在第一项的列表中找到和自己对应相等的. 

利用 map 键值对匹配的结构, 将所有的第一项放在 map 的键的位置, 值位可以用 1 代替.

即得到如下的 map:

```
"第一项" - 1
"第二项" - 1
"第三项" - 1
```

由于非目的地总能在其中找到相等的, 所以利用这一特点, 把第二项依次代入键到其中查找, 如果取出键值为空, 说明没有在其中找到匹配的第一项, 也就是起点项. 那正满足最终目的地的条件.





#### Code

```java
class Solution {
    public String destCity(List<List<String>> paths) {
        Map<String, Integer> map = new HashMap<String, Integer>();  // <String, Integer>
        for (List<String> list : paths)      //  path 的项为一个 List<Map>
            map.put(list.get(0), 1);        //   项的第一项当作 key, 1 当作 value
        //  "第一项" - 1
        //  "第二项" - 1
        //  "第三项" - 1
        for (List<String> list : paths)
            if (map.get(list.get(1)) == null)   //  以 path 其中第二项的作为 key 去 由第一项组成的 map 里面取
            // 如果第二项对应的 value 为空, 找不到第二项对应的第一项, 那它就是终点了
                return list.get(1);             //  则返回它
        return null;
    }
}
```

效果:

执行结果：

通过

显示详情

执行用时：2 ms, 在所有 Java 提交中击败了99.94%的用户

内存消耗：39.6 MB, 在所有 Java 提交中击败了30.83%的用户





commit 1

> 我原意是想将这个列表转化成一个二维数组, 然后利用两层循环在所有的第一项中找和第二项值相等的字符串, 可以编译错误, 语法出了问题. 还是这个用 map 的方法 diao

commit 2

commit 3





