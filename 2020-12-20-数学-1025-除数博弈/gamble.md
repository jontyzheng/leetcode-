#### Question [1025. 除数博弈](https://leetcode-cn.com/problems/divisor-game/)

tag##



#### Description

```
爱丽丝和鲍勃一起玩游戏，他们轮流行动。爱丽丝先手开局。

最初，黑板上有一个数字 N 。在每个玩家的回合，玩家需要执行以下操作：

选出任一 x，满足 0 < x < N 且 N % x == 0 。
用 N - x 替换黑板上的数字 N 。
如果玩家无法执行这些操作，就会输掉游戏。

只有在爱丽丝在游戏中取得胜利时才返回 True，否则返回 False。假设两个玩家都以最佳状态参与游戏。

 

示例 1：

输入：2
输出：true
解释：爱丽丝选择 1，鲍勃无法进行操作。
示例 2：

输入：3
输出：false
解释：爱丽丝选择 1，鲍勃也选择 1，然后爱丽丝无法进行操作。
 

提示：

1 <= N <= 1000

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/divisor-game
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```







#### Code

```java
class Solution {
    //执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
    public boolean divisorGame(int N) {
        return N%2 == 0;
    }
}
```







#### 分析

给定一个数, 然后双方轮流报一个因子数, 每次报完因数后, 令 N 等于 N 与因数作差, 更新 N, 作为下一轮对方要拿到的数字.

由于每次的因子的限定条件是: 最小为 1, 最大不得超过数字本身.

所以每次, 当最后拿到 1 的一方, 因为无法拿出符合条件的因子而宣告输掉比赛.



文中有一句话十分关键 - "假设双方都以最佳状态参加比赛".

说明, 每次双方都是选对自己最有利的因子. 

这也呼应了前面"双方可以任意选其中一个因子"的话.



<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-12-20-%E6%95%B0%E5%AD%A6-1025-%E9%99%A4%E6%95%B0%E5%8D%9A%E5%BC%88/IMG_2608(20201220-144416).PNG" width="50%">



通过正确的举例, 也就是每次按照"最佳状态"的样子去报数.

我们可以发现, 有一些出现的情况是必然的:



<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-12-20-%E6%95%B0%E5%AD%A6-1025-%E9%99%A4%E6%95%B0%E5%8D%9A%E5%BC%88/IMG_2610(20201220-150838).PNG" width="100%">



比如说: 如果拿到 1 的一方**必然输**.



拿到 2 的时候出 1 **必赢**.



拿到 4 的时候出 1 **必然赢**.



5 的时候**必然只有 1 可以出**. 

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-12-20-%E6%95%B0%E5%AD%A6-1025-%E9%99%A4%E6%95%B0%E5%8D%9A%E5%BC%88/IMG_2607.PNG" width="40%">



6 的时候出 1 **对方必 LOSE**.





7 的时候**必然只能出 1, 然后 LOSE**.







通过标注不同的颜色, 我们发现, 前面几次, 似乎偶数的时候都可以出 **1** 然后拿下比赛.

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-12-20-%E6%95%B0%E5%AD%A6-1025-%E9%99%A4%E6%95%B0%E5%8D%9A%E5%BC%88/IMG_2610(20201220-150838).PNG" width="100%">



于是, 通过列举 8, 10, 12 的例子, 然后列出具体的数字, 发现, 必赢.

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-12-20-%E6%95%B0%E5%AD%A6-1025-%E9%99%A4%E6%95%B0%E5%8D%9A%E5%BC%88/IMG_2612(20201220-150940).PNG" width="70%">

并且, 每次自己拿到的数都是 偶数.

**让对方那拿奇数, 自己就能总拿偶数**. (which which means 2 总是在自己的手上; 对方最后总是拿 1, which means 淘汰)



I. 奇数只能出奇数.

II.奇数相减必为偶数 ( 2 减 1 必 LOSE)

III. 偶数出 1 变奇数抛给对方



每次拿到奇数的一方都比较**被动**.



为了进一步确定规律 我有重新列出了从 3 开始到 9 的奇数.

3, 5, 7 是只能出 1, 然后劣势.

9 为什么每次必 LOSE :

9 有且只有 {1, 3} 因数.

**奇数的因数也只能是奇数**.

那奇数者将一直拿奇数.

一直拿奇数, which means 最后拿到 1.



<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-12-20-%E6%95%B0%E5%AD%A6-1025-%E9%99%A4%E6%95%B0%E5%8D%9A%E5%BC%88/IMG_2613(20201220-151008).PNG" width="40%">





最后, 可以得出结论:

1.并不是每次拿最大因子就有优势.

2.偶数放可以通过出 1 变奇数抛给对方, 然后自己一直拿偶数.

3.拿偶数者可以一直拿偶数, 最后总是拿到 2 (然后将死对方). 拿奇数者一直拿奇数, 最后只能拿 1.

也就是说, 偶数者必赢, 奇数必LOSE. 







#### 测试用例过滤

##### i.4 不一定 Lose

```java
class Solution {
    public boolean divisorGame(int N) {
        //爱丽丝先报一个数x: N的因数 (0,N)
        //修改 N = N - x 后再到对方报数
        //奇数次
        //最佳状态: 每次都去取最大的因数
        //  当 N 为 1 的时候没得找
        if (N == 1)
            return false;
        //  当 N 为 2 的时候必赢
        if (N ==2)
            return true;

        boolean hasWin = false; 
        int cnt = 0;            //  cnt: 轮数

        while (N > 1) {         //  N: 减到值为 1 时退出                       
            //  1.轮数
            cnt++;
            //  2.操作: 求deltaN            
            int x = maxDiv(N);
            if (x == -1) {      //  update: 检查到 -1, 说明 n 的最大的因数为 1, 此时取 1.
                x = 1;
            }
            //  3.作差: 更新 N
            N = N - x;                        
        }

        if (cnt % 2 == 1) 
            hasWin = true;        // 奇数轮: 代表爱丽丝胜利
        else
            hasWin = false;
        return hasWin;
    }

    //  n >= 3
    public int maxDiv(int n) {
        int minDiv = 0;        
        for (int i = 2; i <= n; i++) {
            if (n % i == 0) {
                minDiv = i;                
                break;
            }
        }
        if (minDiv == n)
            return -1;      //  让你去除自己, 如果你检查到你整除的是自己时, 返回 -1
        return n/minDiv;
    }
}
```

> 这个方案的思路:
>
> 假设"**最佳状态**"就是每次让对方的数字越小, 那么就"可能"胜算更大.
>
> 于是, 通过调用一个"寻找最大因数"的方法, 每次调用得到 N-x 中的减数. 
>
> 接着拿给对方.

###### 解释: 4 的方案不是只有 "拿最大因子" 一种

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-12-20-%E6%95%B0%E5%AD%A6-1025-%E9%99%A4%E6%95%B0%E5%8D%9A%E5%BC%88/IMG_2606(20201219-213125).PNG" width="35%">

###### 问题所在: 重新定义"最佳状态"









#### 讲讲你一开始的想法



一开始是是找到爱丽丝在奇数次轮数的点, 然后以为"最佳状态"就是每次报最大的因子, 这样对方的差就越小, 可能越"接近" 1.

但是 4 的测试用例让我发现错误了.

原来, 并不是只会出最大因数的.





#### 本期leetcode	

多找一些"必然出现"的规律.

多找一些通过的规律, 而不是找与前面的数字有关的函数关系. 

通用的关系, 与当前数字本身有关往往会比找与前面数字之间的叠加关系更加复杂.

这是我在第一次列举 10 以后的数字时掉进可以与前面的数字有关陷阱. 因为它看起来可以通过前面已经得到的数字规律上得到最后的胜负结果,

而没有展开所有的因数, 发现自己这一方每次拿的数字都是偶数这一重要的规律.



