#### Question [279. 完全平方数](https://leetcode-cn.com/problems/perfect-squares/)

tag#求和#



#### Description

```
给定正整数 n，找到若干个完全平方数（比如 1, 4, 9, 16, ...）使得它们的和等于 n。你需要让组成和的完全平方数的个数最少。

示例 1:

输入: n = 12
输出: 3 
解释: 12 = 4 + 4 + 4.
示例 2:

输入: n = 13
输出: 2
解释: 13 = 4 + 9.
```



#### Analysis

题目: 给定一个数, 找出最少可以由多少个平方数构成它.



#### Code

```java
class Solution {
    public int numSquares(int n) {  //  求最小组成平方数个数
        if (n<4)
            return n;
        int cnt = 0;
        Queue<Integer> queue = new LinkedList<>();
        boolean[] visited = new boolean[n];

        queue.add(n);   //  queue 里装的是 n
        while ( !queue.isEmpty() ) {
            cnt++;
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                int cur = queue.remove();   //  cur: 对头
                for (int j = 1; j*j<=cur; j++) {    // j: 平方变量
                    if (cur == j*j)
                        return cnt;
                    if ( !visited[cur - j*j]) {
                        visited[cur - j*j] = true;
                        queue.add(cur - j*j);
                    }
                }
            }
        }
        return cnt;
    }
}
```



​			



​			





