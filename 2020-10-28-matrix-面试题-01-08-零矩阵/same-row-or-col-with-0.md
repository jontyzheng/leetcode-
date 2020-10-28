#### Question [面试题 01.08. 零矩阵](https://leetcode-cn.com/problems/zero-matrix-lcci/)

tag#矩阵#



#### Description

```
编写一种算法，若M × N矩阵中某个元素为0，则将其所在的行与列清零。

 

示例 1：

输入：
[
  [1,1,1],
  [1,0,1],
  [1,1,1]
]
输出：
[
  [1,0,1],
  [0,0,0],
  [1,0,1]
]
示例 2：

输入：
[
  [0,1,2,0],
  [3,4,5,2],
  [1,3,1,5]
]
输出：
[
  [0,0,0,0],
  [0,4,5,0],
  [0,3,1,0]
]

```



#### Analysis

做这一题的时候当时是走一步看一步.

分析在做的过程里面.



#### Code

假设坐标含有和 0 项 的行列相同的横纵坐标就置作 0.

commit 1

```java
class Solution {
	// 超时 0 / 159 个通过测试用例
    public void setZeroes(int[][] matrix) {
        int rows = matrix.length;
        int cols = matrix[0].length;
        //  得出 0 元素所在的行号和列号, 再根据得到的行列号变他为 0
        //  找出哪一行要变, 哪一行不要变
        Map<Integer, Integer> map = new HashMap<>();
        //  新建一个容器 map 以 0 出现的横坐标作为k, 纵坐标作为v 存储
        //  遍历矩阵, 将与它们非同行非同列的保留原值
        for (int i=0; i<rows; i++) {
            for (int j=0; j<cols; j++) {
                if (matrix[i][j] == 0) {
                    map.put(i, j);
                }
                
            }
        }
        for (int i=0; i<rows; i++) {
            for (int j=0; i<cols; j++) {
                if (map.get(i) != null || map.get(j) != null) {
                    matrix[i][j] = 0;
                }
            }
        }        
    }
}
```

> 假设是因为 map 可以根据 key 找 value, 也可能根据 value 找 key.
>
> 且超时时间是因为经过了两轮循环.

![](https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-10-28-matrix-%E9%9D%A2%E8%AF%95%E9%A2%98-01-08-%E9%9B%B6%E7%9F%A9%E9%98%B5/set-store.PNG)



commit 2

```java
class Solution {
    // 23 / 159 个通过测试用例
    public void setZeroes(int[][] matrix) {
        int rows = matrix.length;
        int cols = matrix[0].length;
        //  得出 0 元素所在的行号和列号, 再根据得到的行列号变他为 0
        //  找出哪一行要变, 哪一行不要变
        // Map<Integer, Integer> map = new HashMap<>();    
        Set<Integer> set = new HashSet<>();
        //  改用 set 容器, 先后加入 0 所在的横纵坐标, 只要取出不为空, 视为和 0 同行或同列, 置为 0
        //  遍历矩阵, 将与它们非同行非同列的保留原值
        for (int i=0; i<rows; i++) {
            for (int j=0; j<cols; j++) {
                if (matrix[i][j] == 0) {
                    set.add(i);
                    set.add(j);
                }
                if (set.contains(i) == true | set.contains(j) == true) {
                    matrix[i][j] = 0;
                }
            }
        }              
    }
}
```

> 改成 set, 并且将第二轮匹配的循环合并到第一轮添加 0 元素行列的循环里.



未通过用例:

```
1,1,1	-	1,1,1
1,0,1	-	1,0,0
1,1,1	-	1,0,1
```

![](https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-10-28-matrix-%E9%9D%A2%E8%AF%95%E9%A2%98-01-08-%E9%9B%B6%E7%9F%A9%E9%98%B5/the-former-lost-check.PNG)

排在前面的就没有被检验到





commit 3

先遍历, 加入所有横纵坐标再取出匹配

```java
class Solution {
    // 48 / 159 个通过测试用例
    public void setZeroes(int[][] matrix) {
        int rows = matrix.length;
        int cols = matrix[0].length;
        //  得出 0 元素所在的行号和列号, 再根据得到的行列号变他为 0
        //  找出哪一行要变, 哪一行不要变
        // Map<Integer, Integer> map = new HashMap<>();    
        Set<Integer> set = new HashSet<>();
        //  改用 set 容器, 先后加入 0 所在的横纵坐标
        //  只要取出不为空, 视为和 0 同行或同列, 置为 0        
        for (int i=0; i<rows; i++) {
            for (int j=0; j<cols; j++) {
                if (matrix[i][j] == 0) {
                    set.add(i);
                    set.add(j);
                }                
            }
        } 
        //  遍历矩阵, 将与它们同行同列的置为 0
        for (int i=0; i<rows; i++) {
            for (int j=0; j<cols; j++) {
                if (set.contains(i) == true | set.contains(j) == true) {
                    matrix[i][j] = 0;
                }                 
            }
        }                    
    }
}
```

未通过的用例:

```
0,0,0,3	-	0,0,0,0	+	0,0,0,0
4,3,1,4	-	0,0,0,0	+	0,0,0,4
0,1,1,4	-	0,0,0,0	+	0,0,0,0
1,2,1,3	-	0,0,0,3	+	0,0,0,3
0,0,1,1	-	0,0,0,0	+	0,0,0,0
```

第二列的最后一个 4 怎么没了呢? 

仔细看这个测试用例, 可以发现, 并不是说 (x,y) 有一个和 0 的横纵坐标重合就该置为 0.

而是, 和 0 在同一行, 或者和 0 同一列, 才会被扫射成 0.

这说明

1.要分别找出 0 所在的行和列, 

2.然后拿 (x,y) 的横坐标到行列表中匹配, 纵坐标到行列表匹配.

3.只要是有一个匹配, 就应该被置 0.

![](https://github.com/jontyzheng/leetcode-journal/blob/master/2020-10-28-matrix-%E9%9D%A2%E8%AF%95%E9%A2%98-01-08-%E9%9B%B6%E7%9F%A9%E9%98%B5/where-the-question-is.PNG)



commit 4

```java
class Solution {
    // 执行用时：3 ms, 在所有 Java 提交中击败了17.45%的用户
    // 内存消耗：40.1 MB, 在所有 Java 提交中击败了75.65%的用户
    public void setZeroes(int[][] matrix) {
        int rows = matrix.length;
        int cols = matrix[0].length;
        //  得出 0 元素所在的行号和列号, 再根据得到的行列号变他为 0
        //  找出哪一行要变, 哪一行不要变
        // Map<Integer, Integer> map = new HashMap<>();    
        Set<Integer> rowsSet = new HashSet<>();
        Set<Integer> colsSet = new HashSet<>();
        //  改用 set 容器, 先后加入 0 所在的横纵坐标, 只要取出不为空, 视为和 0 同行或同列, 置为 0
        //  遍历矩阵, 将与它们非同行非同列的保留原值
        for (int i=0; i<rows; i++) {
            for (int j=0; j<cols; j++) {
                if (matrix[i][j] == 0) {
                    rowsSet.add(i);
                    colsSet.add(j);
                }                
            }
        } 
        for (int i=0; i<rows; i++) {
            for (int j=0; j<cols; j++) {
                if (rowsSet.contains(i) == true | colsSet.contains(j) == true) {
                    matrix[i][j] = 0;
                }                 
            }
        }                    
    }
}
```

>  拿一个哈希表保存 0 所出现的行, 一个哈希表保存列.





​			





