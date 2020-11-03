#### Question [349. 两个数组的交集](https://leetcode-cn.com/problems/intersection-of-two-arrays/)

tag#数组# #找两个数据的重合部分# #集合#



#### Description

```
给定两个数组，编写一个函数来计算它们的交集。

 

示例 1：

输入：nums1 = [1,2,2,1], nums2 = [2,2]
输出：[2]
示例 2：

输入：nums1 = [4,9,5], nums2 = [9,4,9,8,4]
输出：[9,4]
 

说明：

输出结果中的每个元素一定是唯一的。
我们可以不考虑输出结果的顺序。
```



#### Analysis

已知两个数组, 找它们都含有的数据.

可以先退出来想, 如果手上已经有一个集合, 集合里有许多个元素.

然后要从另外一个集合中找, 和自己集合中已有元素相等的元素. 找到后把它们给收集起来.

从一个集合中查找, 不正是 map 最擅长的事情吗

然后, 既然是从一个集合中找到, 找自己集合相等的元素.

首先, 将其中任意一个集合放进 map 中. 构成一个查找容器.

然后怎么保证键值可以让两个相等得元素之间互相查找呢? 就可以以这个元素的值为 key, 

value 不可能是 0~i 之类的, 加了也没用, 又不能完全没有规律. 这时候为什么不可以将这个元素的值同时作为 value. 这样, 查找的返回值也能另外拿来匹配, 一举两得.

于是, 大致的方案就出来了.





#### Code

##### commit 1

##### 找到两个数组重合的部分

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        //  找交集
        Map<Integer, Integer> map = new HashMap<>();
        List<Integer> list = new ArrayList<>();
        int len1 = nums1.length;
        int len2 = nums2.length;
        for (int i = 0; i < len1; i++) {
            map.put(nums1[i], nums1[i]);
        }
        for (int j = 0; j < len2; j++) {
            int target = nums2[j];
            if (map.get(target) != null) {
                list.add(target);                
            }            
        }
        int[] newArr = new int[list.size()];
        for (int i = 0; i < list.size(); i++) {
            newArr[i] = list.get(i);
        }
        return newArr;
    }
}
```



接着, 想办法不重复添加就好了

##### 改进

前提: 当前元素是两个集合都包含的元素 - 集合 B 中的元素可以在以 集合 A 元素为 key 为 value 的 map 中匹配到对应的值.

1.第一个的时候无需考虑是否重复添加.

2.当列表不为空的时候除了交集, 还需保证列表中之前没有该元素, 以保证不重复添加.

##### commit 2

```java
class Solution {
    //执行用时：8 ms, 在所有 Java 提交中击败了13.39%的用户
    //内存消耗：39 MB, 在所有 Java 提交中击败了48.80%的用户
    public int[] intersection(int[] nums1, int[] nums2) {
        //  找交集
        Map<Integer, Integer> map = new HashMap<>();
        List<Integer> list = new ArrayList<>();
        int len1 = nums1.length;
        int len2 = nums2.length;
        for (int i = 0; i < len1; i++) {
            map.put(nums1[i], nums1[i]);
        }        
        for (int j = 0; j < len2; j++) {
            int target = nums2[j];            
            if (map.get(target) != null) {       
                //	在列表为空的时候默认添加
                if (list.size() == 0)
                    list.add(target);
                //	不为空的时候还需检验是否原先包含该元素
                else if (list.size() != 0 && !list.contains(target))                                                         list.add(target);                               
            }            
        }
        int[] newArr = new int[list.size()];
        for (int i = 0; i < list.size(); i++) {
            newArr[i] = list.get(i);
        }
        return newArr;
    }
}
```



​			





