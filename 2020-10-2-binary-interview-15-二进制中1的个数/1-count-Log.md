#### Question [剑指 Offer 15. 二进制中1的个数](https://leetcode-cn.com/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/)

tag##



#### Description



#### Analysis





#### Code

```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
                
        List<Integer> list = new ArrayList<>();
        while (n!=0) {
            int num = n%10;            
            if (num==1) 
                list.add(num);
            n = n/10;
        }
        return list.size();
    }
}
```

> 感觉有戏





