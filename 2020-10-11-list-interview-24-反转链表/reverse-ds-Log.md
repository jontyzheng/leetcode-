#### Question [剑指 Offer 24. 反转链表](https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/)

tag#剑指 offer# #链表# #反转#



#### Description

```
定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

 

示例:

输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
 

限制：

0 <= 节点个数 <= 5000

```

**注意**：本题与主站 206 题相同：https://leetcode-cn.com/problems/reverse-linked-list/



#### Analysis

利用栈反转到链表. push 后的最后一个作为新的 newHead, 通过栈的 pop 不断弹出上一个结点.



#### Code

栈的运用

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
    public ListNode reverseList(ListNode head) {
        // 执行用时：2 ms, 在所有 Java 提交中击败了8.39%的用户
        // 内存消耗：38.7 MB, 在所有 Java 提交中击败了43.94%的用户
        if (head == null) return null;
        Stack<ListNode> nodeStack = new Stack<>();
        while (head != null) {
            nodeStack.push(head);
            head = head.next;
        }
        ListNode newHead = nodeStack.pop(); //  将 pop 出的结点当作新的头结点        
        ListNode newTail = newHead;        //  复制一份, 保留后面作罪
        while (!nodeStack.isEmpty()) {      
            ListNode popped =  nodeStack.pop();     
            newTail.next = popped;         //  延续上一次的 tailNode.next
            newTail = popped;  
        }
        newTail.next = null;
        return newHead;
    }
}
```

第一次正式使用栈来解决问题.



