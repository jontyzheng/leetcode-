#### Question 完数

tag##



#### Description

```
如果一个数恰好等于它的真因子之和，则称该数为“完全数”。

例如, 6 的真因子为 1,2,3, 而6=1+2+3, 因此 6 是"完全数".

编程求出 1000 以内的所有完数.

By 蔡同学
```





#### Analysis

完数的概念: 如果一个数的所有因子之和(不包括本身)等于改该数字, 则视为一个完全数(Perfect Number).

给定范围找出其中的完全数, 一定会用到遍历, 对该范围的每一个数字进行判断.

1.找出一个数的所有因子是必须的. 最后这个因子之和才可以和数字本身进行匹配.

2.找出因子可以用最简单的依次遍历判断 n%i == 0. 如果整除的话, 将两个都加入到集合中去.

3.因子求和可以另外开一个方法.

4.主方法中先后调用前两个方法, 拿因子之和和原数字判等, 如果相等, 就满足条件, 可添加到结果集合中.



另外注意:

1.拿 6 为例, 如果 6/2 == 3. 两个因子都要添加.

2.为防止重复添加, 可以用 Set 集合.

3.最后移除掉数字本身.



#### Code

代码将分为 3 个子方法

1.`findDivisor(int x)` :  Set<Integer> 找因子;

2.`sum(Set<Integer> set)`: int 求和

3.`findPerfectNumber(int n)`: List 验证完全数

```java
/**
 * @author Jonty Zheng
 */

public class AllDivisor {
    public static void main(String[] args) {
        List<Integer> perfectList = findPerfectNumber(1000);
        if (perfectList.size() == 0)
            System.out.println("区间(0, " + 1000 + "]之间不存在完全数");
        else  {
            for (Integer i : perfectList) {
                System.out.println(i);
            }
        }
    }

    //  验证完全数, 可以用 List
    public static List findPerfectNumber(int n) {
        List<Integer> list = new ArrayList<>();
        for (int i = 1; i < n; i++) {
                Set<Integer> divisorSet = findDivisor(i);
                if (sum(divisorSet) == i)
                    list.add(i);
        }
        return list;
    }

    //  找因子, 建议用 Set, 不重复集合
    public static Set<Integer> findDivisor(int x) {
        Set<Integer> set = new HashSet<>();
        for (int i = 1; i < x; i++) {
            if (x%i == 0) {
                set.add(i);
                set.add(x/i);
                //break;
            }
        }
        set.remove(x);  // 真因子不包括 x 本身
        return set;
    }

    //  因子求和
    public static int sum(Set<Integer> set) {
        int sum = 0;
        if (set.size() == 0);
        else {
            for (Integer e : set) {
                sum += e;
            }
        }
        return sum;
    }
}

```





##### 【本期小结】

常规思路



