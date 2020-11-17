#### Question [859. 亲密字符串](https://leetcode-cn.com/problems/buddy-strings/)

tag##



#### Description [859. 亲密字符串](https://leetcode-cn.com/problems/buddy-strings/)

```
给定两个由小写字母构成的字符串 A 和 B ，只要我们可以通过交换 A 中的两个字母得到与 B 相等的结果，就返回 true ；否则返回 false 。

交换字母的定义是取两个下标 i 和 j （下标从 0 开始），只要 i!=j 就交换 A[i] 和 A[j] 处的字符。例如，在 "abcd" 中交换下标 0 和下标 2 的元素可以生成 "cbad" 。

 

示例 1：

输入： A = "ab", B = "ba"
输出： true
解释： 你可以交换 A[0] = 'a' 和 A[1] = 'b' 生成 "ba"，此时 A 和 B 相等。
示例 2：

输入： A = "ab", B = "ab"
输出： false
解释： 你只能交换 A[0] = 'a' 和 A[1] = 'b' 生成 "ba"，此时 A 和 B 不相等。
示例 3:

输入： A = "aa", B = "aa"
输出： true
解释： 你可以交换 A[0] = 'a' 和 A[1] = 'a' 生成 "aa"，此时 A 和 B 相等。
示例 4：

输入： A = "aaaaaaabc", B = "aaaaaaacb"
输出： true
示例 5：

输入： A = "", B = "aa"
输出： false
 

提示：

0 <= A.length <= 20000
0 <= B.length <= 20000
A 和 B 仅由小写字母构成。


```



#### Analysis

##### 1.亲密字符串是什么?

给定两个字符串, 双方可以通过 2 个位置上的字符相互转换(匹配)即互相亲密.

##### 2.具体是什么意思?

1.长度至少在 2 以上才能交换 **2** 个字符;

2.长度不相等的怎么交换都不会互相相等;

所以必备的条件有 

①长度大于等于 2; ②长度一致;

一些特殊情况:



| 特殊情形  | 亲密程度 | 解释                                      |
| --------- | -------- | ----------------------------------------- |
| aaa aaa   | √        | 都是由同一个字母组成的, 可任意交换        |
| ab ab     | ×        | 完全相同的字符串, 交换后便不同了          |
| abab abab | √        | 完全相同, 有 2 个以上相同的字符可任意交换 |
| abcd abcd | ×        | 完全相同, 但是 4 个字符各不相同           |



一步步排除掉这些特殊的情况就可以了



#### Code

```java
class Solution {
    //执行用时：3 ms 29 / 29 个通过测试用例
    public boolean buddyStrings(String A, String B) {
        int len1 = A.length();
        int len2 = B.length();
        //  • 长度不相同的不亲密
        //  • 长度在 2 以下的不存在亲密的条件
        if (len1 != len2 || len1 < 2 || len2 < 2)
            return false; 
        //  • 字符串相等, 并且都是由同一个字母构成的绝对亲密
        if (A.equals(B) && (isConsistOfOneAlpha(A) == true || isConsistOfOneAlpha(B) == true))       
            return true;        
        //  • 字符串相等, 至少包含 2 个以上可交换的相同字符绝对亲密
        if (A.equals(B)) {
            if ( hasTwoMoreInCommon(A) == true || hasTwoMoreInCommon(B) == true )
                return true;
            return false;
        }    
        //  • 排除前面绝对亲密的情形, 亲密的字符串不相同的个数只能是 2 个, 而且它们要交叉相等                        
        List<Character> specialInA = new ArrayList<>();
        List<Character> specialInB = new ArrayList<>();
        for (int i = 0; i < len1; i++) {
            if (A.charAt(i) != B.charAt(i)) {
                specialInA.add(A.charAt(i));
                specialInB.add(B.charAt(i));
            }
        }          
        //  • 用 2 个链表保存双方不相同的地方,  不相同的地方可能超过 2 或者只有 1 个字符有差别
        if (specialInA.size() != 2 || specialInB.size() != 2) 
            return false; 
        //  • 2 个差异字符所处的位置不交叉, 不能通过交换匹配也直接排除           
        if (specialInA.get(0) != specialInB.get(1) || specialInA.get(1) != specialInB.get(0))
            return false;
        return true; 
    }

    public boolean isConsistOfOneAlpha(String s) {
        boolean isConsistOfOneAlpha = true;
        char a = s.charAt(0);
        for (char c : s.toCharArray()) {
            if (c != a) {
                isConsistOfOneAlpha = false;
                break;
            }
        }
        return isConsistOfOneAlpha;
    }

    public boolean hasTwoMoreInCommon(String s) {
        boolean hasTwoMoreInCommon = false;
        String ss = s;
        char[] charArr = ss.toCharArray();
        Arrays.sort(charArr);
        int count = 0;
        for (int i = 0; i < s.length()-1; i++) {
            if (charArr[i] == charArr[i+1]) {
                return true;
            }
        }
        if (charArr[s.length()-1] == charArr[s.length()-2])
            hasTwoMoreInCommon = true;
        return hasTwoMoreInCommon;
    }
}
```





#### 本期心情						

一步步排除



