#### Question [面试题 16.11. 跳水板](https://leetcode-cn.com/problems/diving-board-lcci/)

tag##



#### Description

```
你正在使用一堆木板建造跳水板。有两种类型的木板，其中长度较短的木板长度为shorter，长度较长的木板长度为longer。你必须正好使用k块木板。编写一个方法，生成跳水板所有可能的长度。

返回的长度需要从小到大排列。

示例 1

输入：
shorter = 1
longer = 2
k = 3
输出： [3,4,5,6]
解释：
可以使用 3 次 shorter，得到结果 3；使用 2 次 shorter 和 1 次 longer，得到结果 4 。以此类推，得到最终结果。
提示：

0 < shorter <= longer
0 <= k <= 100000

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/diving-board-lcci
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```







#### Code

```java
class Solution {
    //执行用时：1 ms, 在所有 Java 提交中击败了100.00%的用户
    public int[] divingBoard(int shorter, int longer, int k) {         
        //  k == 0
        if (k == 0)
            return new int[0];
        //  shorter == longer
        if (shorter == longer) 
            return new int[]{shorter*k};
        //  k+1 项       
        int[] boardArr = new int[k+1];
        //  x*shorter + y*longer
        for (int i = 0; i <= k; i++) {
            boardArr[i] = longer*i + shorter*(k-i);
            //boardArr[i] = shorter*k + (longer-shorter)*i;
        }
        return boardArr;
    }
}
```







#### 分析

##### 题目的概念

题目说的是"有一堆", 一共 2 种, 现在你只需要 k 块, 可以根据自己的需要从中任意选来拼接.

再具体一点, 就是默认长短木板要多少有多少. 长短木板自助.



##### 推理

为什么答案都说:

最后可能的结果数是 `k+1` 种呢?

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-12-27-%E8%B7%B3%E6%B0%B4%E6%9D%BF-%E9%9D%A2%E8%AF%95%E9%A2%98-16-11-%E8%B7%B3%E6%B0%B4%E6%9D%BF/k_1.PNG" zoom="5%"/>



当确定数组长度之后, 就可以初始化数组长度了.



由于短木板和长木板可能相等, 所以存在 2 种情况:

① 长短木板相等, 那么只有一种情况: `shorter * k`

② 组合: 短木板 * x + 长木板 * (k-x).

最小长度一一定是全为短木板 `shorter*k`

之后 `x` 依次递减, 给一块给长木板, 最后当所有木板都为长木板时达到最高长度.

> 所以这里的 for 循环终点应该是从 0 开始, 以 k 结束.



最后的解决方案可以分成下面 3 步:

1.k 是否为 0: 如果为 0, 则返回 []

2.shorter 和 longer 是否相等: 相等则只有一种情况

3.`shorter * i + longer * (k - i)`: i 总是从 k 开始递减, 到 0.





#### 测试用例过滤

###### I.没找到结果长度的数量规律

```java
class Solution {
    public int[] divingBoard(int shorter, int longer, int k) {
        List<Integer> list = new ArrayList<>();   
        int[] arr = new int[0];
        if (k == 0)         
            return arr;
        for (int i = 0; i < k; i++) {
            int x = k - i;                      //  x 从大到小递减
            int y = i;
            int sum = shorter * x + longer * y;            
            if (list.contains(sum) == false)    //  去重
                list.add(sum);
        }
        if (list.contains(longer*k) == false)   //  验证
            list.add(longer * k);
        return list.stream().mapToInt(Integer::intValue).toArray();        
    }


}
```



> ```
> 55 / 60 个通过测试用例
> 状态：超出时间限制
> 提交时间：几秒前
> 最后执行的输入：
> 9
> 8436
> 28489
> ```
>
> 





###### II.以为是递归

```java
class Solution {    
    public int[] divingBoard(int shorter, int longer, int k) {
        List<Integer> list = new ArrayList<>();   
        int[] arr = new int[0];                 //  [] 返回
        if (k == 0)         
            return arr;   
        if (shorter == longer)
            return new int[]{shorter*k};        //  一种可能
        int x = 0;
        int sum = 0;
        list.add(turtle(shorter, longer, k, x));

        return list.stream().mapToInt(Integer::intValue).toArray();        
    }

    public int turtle(int a, int b, int k, int x) {        
        if (x == k+1) {
            return 0;
        }
        else {                        
            int sum = 0;
            sum = a*x + b*(k-x);            
            turtle(a, b, k, ++x);
            return sum;
        }        
    }
}
```



> ```
> 2 / 60 个通过测试用例
> ```
>
> 还分析了每一次的主要步骤
>
> 看了评论区一位老哥的吐槽才开始觉得不对啊, 有毛病



###### III.参考另一位与我原本思路相同的答案

```java
class Solution {
    //执行用时：1 ms, 在所有 Java 提交中击败了100.00%的用户
    public int[] divingBoard(int shorter, int longer, int k) {         
        //  k == 0
        if (k == 0)
            return new int[0];
        //  shorter == longer
        if (shorter == longer) 
            return new int[]{shorter*k};
        //  k+1 项       
        int[] boardArr = new int[k+1];
        //  x*shorter + y*longer
        for (int i = 0; i <= k; i++) {
            boardArr[i] = longer*i + shorter*(k-i);
            //boardArr[i] = shorter*k + (longer-shorter)*i;
        }
        return boardArr;
    }
}
```



> ```
> 执行结果：通过
> 显示详情  执行用时：1 ms, 在所有 Java 提交中击败了100.00%的用户
> ```
>
> 与 10w 的数量级没关系





#### 讲讲你一开始的想法

一开始想到的也是 `shorter * i + longer * (k - i)`, 但是数组的长度没有确定所以用的还可变数组, 为此还另外看到了一个怎么讲 `List<Integer>` 转 `int[]` 的方法

> ```java
> list.stream().mapToInt(Integer::intValue).toArray();  
> ```
>
> `list`: List<Integer>
>
> `return`: int[]

后来看着题目中标签是递归.

最后还是答案中的方法让我重新回到了一开始没有错的思路上来.





#### 本期leetcode	

很常规的一道组合求和问题.



