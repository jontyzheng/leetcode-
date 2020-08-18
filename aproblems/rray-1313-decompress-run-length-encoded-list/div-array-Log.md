#### Question: [解压缩编码列表](https://leetcode-cn.com/problems/decompress-run-length-encoded-list/)/[Decompress Run-Length Encoded List](https://leetcode-cn.com/problems/decompress-run-length-encoded-list/)



tag#array#



#### Description

```
给你一个以行程长度编码压缩的整数列表 nums 。

考虑每对相邻的两个元素 [freq, val] = [nums[2*i], nums[2*i+1]] （其中 i >= 0 ），每一对都表示解压后子列表中有 freq 个值为 val 的元素，你需要从左到右连接所有子列表以生成解压后的列表。

请你返回解压后的列表。

 

示例：

输入：nums = [1,2,3,4]
输出：[2,4,4,4]
解释：第一对 [1,2] 代表着 2 的出现频次为 1，所以生成数组 [2]。
第二对 [3,4] 代表着 4 的出现频次为 3，所以生成数组 [4,4,4]。
最后将它们串联到一起 [2] + [4,4,4] = [2,4,4,4]。
示例 2：

输入：nums = [1,1,2,3]
输出：[1,3,3]
 

提示：

2 <= nums.length <= 100
nums.length % 2 == 0
1 <= nums[i] <= 100

```



#### Analysis

一个长度确定是偶数的数组, 奇数位存放的是频数 (frequency), 偶数位存放的是实际值 (value). 从第一个开始, 相邻成对的两个数表示 "有 奇数个偶数".

最后的整个数组都是由偶数组成的. 奇数位上的数表示后面偶数的个数 (连续有几个后继的偶数).



方法:

将原数组按照奇偶数依次分成两个小数组, 长度各占一半.

由于最后的偶数个数是奇数数组里的元素总和.

所以对奇数数组 (频数数组) 求和后, 另外申请一个奇数和长度的数组 result.

最后根据奇数数组 (频数数组) 的元素值依次将实际数元素中的值依次赋值给结果数组 result 中.



##### commit 1

1/153

```java
class Solution {
    public int[] decompressRLElist(int[] nums) {
        int[] result;
        int cnt = 0;        
        int[] freq = new int[nums.length/2];	//	奇偶位数组的长度各占一半
        int[] val = new int[nums.length/2];
        int z = 0;
        //	奇偶位数分离, 坐标判别式 ((i+1)%2 != 0) +1还原实际第i位
        for (int i = 0, f = 0, v = 0; i < nums.length; i++) {
            if ((i+1)%2 != 0) {
                freq[f] = nums[i];  
                f++;				//	奇数位数组的pc用f
            }                                                                
            else {
                val[v] = nums[i];	//	偶数位数组的pc用v
                v++;
            }                               
        }
        //	统计最后数组应有的长度
        for (int i = 0; i < freq.length; i++) {
            cnt += freq[i];
        }
        //	初始化目标数组
        result = new int[cnt];
        //	根据赋值
        for (int i = 0, j = 0; i < result.length; i++) {             
            int whilePC = 0;
            //	由于数组元素不存在0. 如果遇到f数组中元素为1时, 不用另外跳位. 单独讨论
            if (freq[j] == 1)
                result[i] = val[j];
            //	以f数组中的元素值为循环终点, 
            else {
                while (whilePC < freq[j]) {
                    result[i] = val[j];
                    i++;
                    whilePC++;                
            	}            
            }    
            j++;	//	if-else一轮后更新一次j
        }
        return result;
    }
}
```



commit 2

**3 / 53** 个通过测试用例

```java
class Solution {
    public int[] decompressRLElist(int[] nums) {
        int[] result;
        int cnt = 0;        
        int[] freq = new int[nums.length/2];
        int[] val = new int[nums.length/2];
        int z = 0;
        for (int i = 0, f = 0, v = 0; i < nums.length; i++) {
            if ((i+1)%2 != 0) {
                freq[f] = nums[i];  
                f++;
            }                                                                
            else {
                val[v] = nums[i];
                v++;
            }                               
        }
        for (int i = 0; i < freq.length; i++) {
            cnt += freq[i];
        }
        result = new int[cnt];
        for (int i = 0, j = 0; i < result.length; i++) { 
            int whilePC = 0;
            if (freq[j] == 1)
                result[i] = val[j];
            else {
                while (whilePC < freq[j]) {
                    result[i] = val[j];
                    i++;
                    whilePC++;                
                }            
            }  
            j++;  				                     
        }
        return result;
    }
}
```

结果:

```
输入
[1,2,3,4]
输出
[2,4,4,4]
预期结果
[2,4,4,4]
```



测试用例分析:

```
执行出错信息：
Line 28: java.lang.ArrayIndexOutOfBoundsException: Index 137 out of bounds for length 137
最后执行的输入：
[65,44,72,15]
```



#### 答案

```java
class Solution {
    public int[] decompressRLElist(int[] nums) {
        int len = 0;
        for(int i = 0; i < nums.length; i += 2){
            len += nums[i];
        }
        int[] res = new int[len];
        int index = 0;
        for(int i = 0; i < nums.length; i+=2){
            while(nums[i] > 0){
                res[index] = nums[i + 1];
                nums[i]--;
                index++;
            }
        }
        return res;
    }
}
```

