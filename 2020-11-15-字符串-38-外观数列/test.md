


先构造整个目标列表, 随后在根据 n 的值从中获取指向项. - 超时

```java
class Solution {
    public String countAndSay(int n) {
        List<StringBuilder> list = makeupTarget();
        return list.get(n-1).toString();
    }

    public List<StringBuilder> makeupTarget() {
        List<StringBuilder> list = new ArrayList<>();   
        String s = "1";
        //list.add(new StringBuilder(s));
        for (int i = 1; i <= 30; i++) {        
            if (i == 1)
                list.add(new StringBuilder(s));
            else {
                StringBuilder thisSbu = new StringBuilder();

                for (int j = 0; j < s.length(); j++) {
                    int count = 1;                                 
                    char value = s.charAt(j);
                    if ( (j+1) < s.length()) {                   
                        if (s.charAt(j+1) == value) 
                            count++;
                        else
                            thisSbu.append(count);
                            thisSbu.append(value);                
                    } 
                    else {
                        thisSbu.append(count);   //  是可以直接追加数字的
                        thisSbu.append(value);
                    }                
                    list.add(thisSbu);  
                    s = thisSbu.toString();       //  每次更新 s
                }
            }            
        }
        return list;            
    }
}
```

> 超时是因为每次更新 s 都是在当前循环内执行的, 一直拿新的字符串给它循环, 当然会永远循环下去.
>
> 字符串一直更新, 字符串终点随之扩增, 循环也随之不断进行下去.

解决方法: s 的更新放在当前循环结束外(新的字符串)
