#### Question [剑指 Offer 50. 第一个只出现一次的字符](https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/)

tag##



#### Description



#### Analysis





#### Code

```java
class Solution {
    public char firstUniqChar(String s) {
        int len = s.length();
        String coped = s;
        char[] arr = s.toCharArray();
        Arrays.sort(s);
        for (int i=1; i<len; i++) {
            if (arr[i] == arr[i-1]) {
                arr[i-1] = ' ';
                arr[i] = ' ';
            }
        }
        for (int i=0; i<len; i++) {
            boolean showed = false;
            for (int j=0; j<len; j++) {
                if (coped.charAt(i) == arr[j]) {
                    showed = true;
                    break;
                }
            }
            if (!showed) {
                
            }
        }
    }
}
```







