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



day2: 

```java
class Solution {
    public String reverseStr(String s, int k) {
        int len = s.length();
        String target;
        if (len == 1)
            return s;
        int span = 2*k;     //  跨度       
        int how_many_parts = ? len/span : len/span + 1;  //  不够整除            
        int i_end = len/span;
        
        //  开头只有不完整的情况        
        if (1 < len < k) {
            return new StringBuilder(s).reverse().toString();
        }
        //  如果在 k+1 到一个 span 长度的范围内, 只反转前 k 项
        StringBuilder sbu;
        if (k+1 <= len <=span) {
            sbu = new StringBuilder();
            //  先追加前两项, 反转后追加后面的 span-k 项
            for (int i = 0; i < len; i++) {
                if (i < k) 
                    sbu.append(s.charAt(i));
                //  反转后连续追加
                sbu.reverse();
                else {                    
                    sbu.append(s.charAt(i));
                }
            }
            target = sbu.toString();
            return target;
        }
        //  长度大于 2k 项, 需要跨长度的情形
        else {
            //  个数刚好整除的情况
            if (len % span == 0) {
                int z = 0;
                sbu = new StringBuilder();
                while (z < len) {
                    int cnt = 0;
                    if (cnt < span) {
                        if (cnt < k) 
                            sbu.append(s.charAt(cnt));
                        sbu.reverse();
                        else {
                            
                            sbu.append(s.charAt(cnt));
                        }
                        cnt++;
                    }  
                    z++;                                            
                }
                target = sbu.toString();
                return target;
            }
            //  有零头的情况            
            else {
                //  先处理整除 span 部分
                int formerEnd = len - len/span;
                int laterStart = formerEnd + 1;
                int resr = len - 
                int z = 0;
                sbu = new StringBuilder();
                while (z < formerEnd) {
                    int cnt = 0;
                    if (cnt < span) {
                        if (cnt < k) 
                            sbu.append(s.charAt(cnt));
                        sbu.reverse();
                        else {
                            sbu.append(s.charAt(cnt));
                        }
                        cnt++;
                    }
                    z++;                                              
                }                
                //  从最后第一个刚好整除的位置后一位开始, 处理零头部分
                //  基本操作和不够 span 长度的步骤类似
                int y = len - formerEnd + 1;
                StringBuilder subBuilder = new StringBuilder(); //  零头builder, sbu.append(subBuilder.toString());
                //  rest 刚好为 1: 零头builder直接追加
                if (rest == 1) {
                    subBuilder.append(sbu.append(s.charAt(y));
                }
                //  rest 介于 2 ~ span 之间: 零头buidler追加后反转
                else if (1 < rest <= k) {                    
                    subBuilder.append(s.charAt(y));
                    y++;
                }
                subBuilder.reverse();
                // rest 介于 k+1 ~ span 之间: 零头builder追加反转后追加
                else { 
                    while (y < len) {
                        int w = 0;
                        if (w < k) {
                            subBuilder.append(s.charAt(y+w));
                        }
                        subBuilder.reverse();
                        else {
                            subBuilder.append(s.charAt(y+w));
                        }
                        w++;
                    }
                    int cnt = 0;
                    if (cnt < span) {
                        if (cnt < k) 
                            sbu.append(s.charAt(cnt));
                        sbu.reverse();
                        else {s.charAt(cnt)
                            sbu.append(s.charAt(cnt));
                        }
                        cnt++;
                    } 
                    int w = 0;                  
                    if ()
                        StringBuilder subBuilder
                        if (i <= k) {
                            
                        }
                    }
                }
                if ()
                target = sbu.toString();
                return target;
            }
                               

        }
            

        }        
        
        //  还有余数的情况        
    }

    //  单独写一个方法调用 - 字符串连续
}
```





#### Code



#### 本期心情						





