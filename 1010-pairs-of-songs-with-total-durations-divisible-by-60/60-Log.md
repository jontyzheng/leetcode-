### Question title: [Pairs of Songs With Total Durations Divisible by 60](https://leetcode-cn.com/problems/pairs-of-songs-with-total-durations-divisible-by-60/)/[总持续时间可被 60 整除的歌曲](https://leetcode-cn.com/problems/pairs-of-songs-with-total-durations-divisible-by-60/)



tag#array#



### Description

```
在歌曲列表中，第 i 首歌曲的持续时间为 time[i] 秒。

返回其总持续时间（以秒为单位）可被 60 整除的歌曲对的数量。形式上，我们希望索引的数字 i 和 j 满足  i < j 且有 (time[i] + time[j]) % 60 == 0。

 

示例 1：

输入：[30,20,150,100,40]
输出：3
解释：这三对的总持续时间可被 60 整数：
(time[0] = 30, time[2] = 150): 总持续时间 180
(time[1] = 20, time[3] = 100): 总持续时间 120
(time[1] = 20, time[4] = 40): 总持续时间 60
示例 2：

输入：[60,60,60]
输出：3
解释：所有三对的总持续时间都是 120，可以被 60 整数。
 

提示：

1 <= time.length <= 60000		//	数量超过 e^5
1 <= time[i] <= 500
```



#### Analysis

问题很清晰: 在给定的整数数组中找出两两之和被 60 整除的对数.

常规思路: 是找出所有可能的组合 (1+1), 对和求余判断后加加, 最后返回计数器.

缺点: 超时



#### Code

32/34: 超时

```java
class Solution {
    public int numPairsDivisibleBy60(int[] time) {
        int sum = 0;
        int cnt = 0;
        if (time.length == 1){            
                return 0;
        }            
        for (int i = 0; i < time.length; i++) {            
            for (int j = i + 1; j < time.length; j++) {
                if ((time[i] + time[j]) % 60 == 0)                    
                    cnt++;
            }
        }
        return cnt;
    }
}
```

> 减少找到所有对数组合的次数



尝试 "假如每一个都是 60 的倍数, 那么返回长度", 以此来尽可能减少这种可能情形的时间. 

> 因为只能另外开一轮遍历逐个判断, 等于在原来的基础上再去增加时间的消耗.





一个小数字加上一个大数字之和也可以组成 60 的倍数, 而小数%大数的结果是 ~~`0`~~.

> 求余运算法则, 被除数小于除数的求余结果得到**小数**
>
> 除非为 0, 否则当组合之和小于 60 的时候说明不可能被 60 整除.
>
> 但仍然要当前循环对符合情况的组合进行判断. 在执行上并没有步骤的压缩.

```java
class Solution {
    public int numPairsDivisibleBy60(int[] time) {        
        int cnt = 0;
        int pairSum = 0;
        if (time.length == 1){            
                return 0;
        }  
               
        for (int i = 0; i < time.length; i++) {            
            for (int j = i + 1; j < time.length; j++) {                
                pairSum = time[i] + time[j];        
                if (pairSum >= 60) {
                    if (pairSum % 60 == 0)          
                        cnt++;
                }
                //  和为小于 60 的不用求余判断                
            }
        }
        return cnt;
    }
}
```

超时

32/34



##### 参考

(20%60 + 100%60) = (20 + 40) % 60 = 0

求余的结果: 可以保证结果不会大于 60.

两个都小于 60 的数字只有在其中一个加上另外一个刚好组成 60 的数字才能继续被 60 整除.

a < 60; b < 60; (a + b) < 2*c (其中 c 为 60).	也就是说 `a` 和 `b` 都小于 60, 它们的和是不会超过 120 的. 和被 60 整除联系起来, 就是要想被 60 整除, 只有刚好等于 60 一种情况.

据分析, 数字a 和 b 对 60 求余过后, 两个数字都小于 60. 

两个小于 60 的数字之和被 60 整除的唯一条件是和为 60. 

感性认识: 求余后就一定小于 60 了; 和为 60 才能继续被 60 整除. 而刚好整除的两个数字任何一个都不会超过 60. 



#### 最终答案

```java
class Solution {
    public int numPairsDivisibleBy60(int[] time) {        
        int res = 0;
        int[] arr = new int[60];        //  index: 余数数值的大小 对应位置上加一

        for (int i = 0; i < time.length; i++) {
            int num = time[i]%60;
            arr[num]++;     //  余数为多少, 哪个位置的数字就加一, 如有几个加几个, 累加在对应余数的位置上, 得到一个由余数个数组成的数组
            time[i] = num;  //  用替换掉原来位置上的数字, 得到一个由余数组成的数组 有 0 有余数
        }

        for (int i = 0; i < time.length; i++) {
            int target = time[i] == 0 ? 0 : 60 - time[i];   //  从余数数组中依次找 0 或差, 依次为 index 到计数数组中找个数
            if (arr[target] != 0) {             //  个数不为 0, 说明先前数组中有对应的数出现过
                res += arr[target];             //  累计上位置上记录过的数
                if (target == 0 || target == 30)  {     //  余数数组中为 0 或者 30 的, 说明原来刚好整除或为 30
                    res -= 1;                           //  此时不再是找差值
                }
            }
        }
        return res / 2;
    }
}
```

