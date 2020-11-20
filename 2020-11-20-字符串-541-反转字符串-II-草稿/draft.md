#### Question [541. 反转字符串 II](https://leetcode-cn.com/problems/reverse-string-ii/)

tag##



#### Description



#### Analysis

```java
class Solution {
    public String reverseStr(String s, int k) {
        int len = s.length();
        if (len == 1)
            return s;
        int span = 2*k;     //  跨度       
        int how_many_parts = ? len/span : len/span + 1;  //  不够整除            
        int i_end = len/span;
        
        //  开头只有不完整的情况
        
        for (int i = 0; i < i_end; i ++) {
            for (int j = 0; j < span; j++) {
                char c = s.charAt(i).charAt(j);
                int x = 0;
                while (x < k) {
                    list.get(1).append(c);
                }
                
            }            
        }
        //  还有余数的情况        
    }

    //  单独写一个方法调用
}
```





#### Code



#### 本期心情						





