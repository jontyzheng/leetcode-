#### Question [剑指 Offer 22. 链表中倒数第k个节点](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)

tag#剑指 offer# #链表#



#### Description

```
输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。例如，一个链表有6个节点，从头节点开始，它们的值依次是1、2、3、4、5、6。这个链表的倒数第3个节点是值为4的节点。

 

示例：

给定一个链表: 1->2->3->4->5, 和 k = 2.

返回链表 4->5.

```



#### Analysis

由示例可得, 倒数第 k 个, 也就是总个数-k+1 个结点.

所以想个办法遍历出原链表中结点的个数, 用 `head = head.next ` 又会覆盖原结点. 所以这里新建一个结点和头结点指向同一个对象即可. 思路不变.



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
    public ListNode getKthFromEnd(ListNode head, int k) {
        //执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
		//内存消耗：37.1 MB, 在所有 Java 提交中击败了5.29%的用户
        int count = 0;
        ListNode temp = head;       //  令临时结点等于头结点
        while (temp.next != null) {      //  当当前结点不为空时, 计数寄存器+1
            count++;                          
            temp = temp.next;       //  如果next域不为空, 继续遍历            
        }
        //  原头结点不变, 又可以遍历所有结点
        //  拿到结点个数, 开始找第 count-k 个结点
        int position = count-k+1;
        int i=1;
        while (i<=position) {
            head = head.next;
            i++;
        }
        return head;
    }
}
```





##### commit 1

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
    public ListNode getKthFromEnd(ListNode head, int k) {
        int count = 0;
        ListNode temp = head;       //  令临时结点等于头结点
        while (temp != null) {      //  当当前结点不为空时, 计数寄存器+1
            count++;
            if(temp.next != null) {                
                temp = temp.next;   //  如果next域不为空, 继续遍历
            }
        }
        //  原头结点不变, 又可以遍历所有结点
        //  拿到结点个数, 开始找第 count-k 个结点
        int position = count-k+1;
        int i=1;
        while (i<=position) {
            head = head.next;
            i++;
        }
        return head;
    }
}
```

> 执行结果：超出时间限制
>
> 直接判断 `temp.next ` 就不用重复那么多了.



#### 技巧

遍历结点个数时判断 temp.next 即可. 如果最后一个为空, 空结点也**不会算进去**.



