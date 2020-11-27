#### Question [415. 字符串相加](https://leetcode-cn.com/problems/add-strings/)

tag#脑筋急转弯#



#### Description

```
给定两个字符串形式的非负整数 num1 和num2 ，计算它们的和。

 

提示：

num1 和num2 的长度都小于 5100
num1 和num2 都只包含数字 0-9
num1 和num2 都不包含任何前导零
你不能使用任何內建 BigInteger 库， 也不能直接将输入的字符串转换为整数形式

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/add-strings
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```



#### Analysis

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-11-27-%E5%AD%97%E7%AC%A6%E4%B8%B2-%20415-%E7%94%A8%E7%A8%8B%E5%BA%8F%E4%BD%9C%E5%8A%A0%E6%B3%95/%E5%88%86%E6%9E%90%E8%BF%87%E7%A8%8B.PNG">



#### Code

```java
class Solution {
    //执行结果：通过 执行用时：3 ms
    public String addStrings(String num1, String num2) {
        int i = num1.length() - 1;
        int j = num2.length() - 1;
        StringBuilder builder = new StringBuilder();
        int add = 0;
        while (i >= 0 || j >= 0 || add != 0) {          //  条件有三: 分别是 i 和 j 还有位数或者 两个都相加完了, 但是还有多出的进位
            int x = i >= 0? num1.charAt(i) - '0' : 0;   //  下标到负数的时候 0 补齐!
            int y = j >= 0? num2.charAt(j) - '0' : 0;
            int result = x + y + add;   /*上一步的 add*/
            add = result/10;            //  add 只取其中十位数
            builder.append(result%10);  //  当前位只取当前位数和的零头
            i--;
            j--;
        }
        builder.reverse(); //  因为 builder 是从后往前追加的, 所以追加的结果反过来才是真正的结果
        return builder.toString();
    }
}
```



##### 测试用例过滤

> 测试用例分析
>
> ```
> 执行结果：
> 解答错误
> 显示详情
> 输入：
> "6913259244"
> "71103343"
> 输出：
> "-1605572005"
> 预期结果：
> "6984362587"
> ```

**154 / 315** 个通过测试用例

```java
class Solution {
    public String addStrings(String num1, String num2) {
        //  数字型字符串转字面上的整数值                
        char[] chars1 = num1.toCharArray();
        char[] chars2 = num2.toCharArray();
        int len1 = chars1.length;
        int len2 = chars2.length;
        int sum1 = 0;
        int sum2 = 0;
        for (int i = 0; i < len1; i++) {
            int value = chars1[i] - '0';            
            sum1 = sum1 * 10;
            sum1 = sum1 + value;
        }
        for (int i = 0; i < len2; i++) {
            int value = chars2[i] - '0';
            sum2 = sum2 * 10;
            sum2 = sum2 + value;
        }
        int sumOfThem = sum1 + sum2;
        return "" + sumOfThem;
    }   
}
```



#### 本期心情						

用程序作竖式加法!



