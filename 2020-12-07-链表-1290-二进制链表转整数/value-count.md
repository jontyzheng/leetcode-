#### Question [1290. 二进制链表转整数](https://leetcode-cn.com/problems/convert-binary-number-in-a-linked-list-to-integer/)

tag#位运算的活用#



#### Description

```
给你一个单链表的引用结点 head。链表中每个结点的值不是 0 就是 1。已知此链表是一个整数数字的二进制表示形式。

请你返回该链表所表示数字的 十进制值 。

 

示例 1：

```

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-12-07-%E9%93%BE%E8%A1%A8-1290-%E4%BA%8C%E8%BF%9B%E5%88%B6%E9%93%BE%E8%A1%A8%E8%BD%AC%E6%95%B4%E6%95%B0/graph-1.png" >

```
输入：head = [1,0,1]
输出：5
解释：二进制数 (101) 转化为十进制数 (5)
示例 2：

输入：head = [0]
输出：0
示例 3：

输入：head = [1]
输出：1
示例 4：

输入：head = [1,0,0,1,0,0,1,1,1,0,0,0,0,0,0]
输出：18880
示例 5：

输入：head = [0,0]
输出：0
 

提示：

链表不为空。
链表的结点总数不超过 30。
每个结点的值不是 0 就是 1。
通过次数36,050提交次数44,425

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/convert-binary-number-in-a-linked-list-to-integer
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```









#### Code

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    //执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
    public int getDecimalValue(ListNode head) {
        ListNode current = head;
        if (current == null)
            return 0;
        int result = 0;
        while (current != null) {
            result = (result << 1) + current.val;
            current = current.next;
        }
        return result;
    }
}
```



#### 分析

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-12-07-%E9%93%BE%E8%A1%A8-1290-%E4%BA%8C%E8%BF%9B%E5%88%B6%E9%93%BE%E8%A1%A8%E8%BD%AC%E6%95%B4%E6%95%B0/shift-operator.jpg">



#### 测试用例过滤

/



#### 出始方案

###### i

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    //超出时间限制
    public int getDecimalValue(ListNode head) {
        StringBuilder builder = new StringBuilder();
        ListNode current = head;
        while (current != null) {
            int x = current.val;
            builder.append('x');
        }
        String str = builder.reverse().toString();
        return stringValue(str);
    }

    public int stringValue(String s) {
        int sum = 0;
        int len = s.length();
        for (int i = 0; i > len; i++) {
            char c = s.charAt(i);
            if (i == 0) {
                if (c == '1') {
                    sum += 1;
                }
            }
            if (c == '1') {
                double newValue = Math.pow(2, i);
                sum += (int)newValue;
            }
        }
        return sum;
    }
}
```

###### ii

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    //超出时间限制
    public int getDecimalValue(ListNode head) {
        List<Integer> list = new ArrayList();
        ListNode revHead = reverse(head);
        int sum = 0;
        while (revHead != null) {
            int x = revHead.val;            
            if (x == 1) {
                int howManyBehind = list.size();
                double newValue = Math.pow(2.0, howManyBehind);
                sum += (int)newValue;
            }
            list.add(x);
        }
        return sum;
    }

    //  反转
    public ListNode reverse(ListNode node) {        
        ListNode pre = new ListNode(-1);
        while (node != null) {
            int value = node.val;
            ListNode preNext = new ListNode(value);
            pre.next = preNext;
            pre = pre.next;            
        }
        return pre.next;
    }
}
```



#### 本期leetcode				

#位运算符新用#



