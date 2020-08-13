#### Question: [子数组最大平均数 I](https://leetcode-cn.com/problems/maximum-average-subarray-i/)/[Maximum Average Subarray I](https://leetcode-cn.com/problems/maximum-average-subarray-i/)

tag#array#



#### Description

```
给定 n 个整数，找出平均数最大且长度为 k 的连续子数组，并输出该最大平均数。

示例 1:

输入: [1,12,-5,-6,50,3], k = 4
输出: 12.75
解释: 最大平均数 (12-5-6+50)/4 = 51/4 = 12.75
 

注意:

1 <= k <= n <= 30,000。
所给数据范围 [-10,000，10,000]。

```



#### Analysis

以 k 个为标准去数组中取固定长度的连续子数组, 找其中平均值最大的子数组也就相当于找总和最大的子数组.





**3 / 123** 个通过测试用例

```java
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        
        int m = nums.length-k+1;      
        int[] target = new int[m];        
        int sum = 0; 
        for (int i = 0; i < m; i++) {   
            for (int j = 0; j < m; j++) {
                sum += nums[j];
            }// 加满 k 个组成 sum   
            target[i] = sum;                           
        }//  装满 k 个组成 target   
        
        //  累加, 所以int都没问题                  
        //  计算 sum 数组中的最大值
        int sumMax = target[0];
        int j = 0;
        while(j < m) {
            if (target[j] > sumMax)
                sumMax = target[j];
            j++;
        }
        return sumMax/k;
    }
}
```

**13 / 123** 个通过测试用例

```java
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        int moveTime = nums.length - k + 1;
        double maxSum = 0;       
        for (int i = 0; i < moveTime; i++) {            
            double sum = 0;
            for (int j = i; j < k; j++) {
                sum += nums[j];
            }
            maxSum = sum > maxSum? sum:maxSum;
        }        
        return maxSum/k;
    }
}
```



#### 答案

```java
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        int[] sums = new int[nums.length+1];
        for (int i=1;i<=nums.length;++i) {
            sums[i] += sums[i-1] + nums[i-1];
        }
        int result = sums[k]-sums[0];
        for (int i=0;i<sums.length-k;++i) {
            int x = sums[i+k] - sums[i];
            result = Math.max(result, x);
        }
        return result*1.0/k;
    }
}
```



​			
