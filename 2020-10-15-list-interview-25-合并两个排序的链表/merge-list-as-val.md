#### Question [剑指 Offer 25. 合并两个排序的链表](https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/)

tag#剑指 offer# #单链表#



#### Description

```
输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

示例1：

输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
限制：

0 <= 链表长度 <= 1000

```

注意：本题与主站 21 题相同：https://leetcode-cn.com/problems/merge-two-sorted-lists/



#### Analysis

一开始看到用例, 我想到的是用一个结点类型的链表, 先对两个单链表中的结点进行比较, 再进行添加, 然后再将链表中的结点一一拼接. 但是两个链表的长度没有想好怎么设置.

如果它们长度不一样的话, 可以比完一个再对那个更长的链表内的项都添加进来.

没有想到 链表遍历后**头结点指向的结点**就是**那个剩余的半条链表**.

后面是参考评论区的.

通过两个一对一比较后, 它用的判空条件是 "若 list1 不为空 && list2 不为空" (正解, 这样才可以一对一比较). 知道如果有剩余的话, 那么那条链表中此时的 head 指向的就是剩余的那半条.

再依次对 list1 和 list2 的头结点进行判空就可以知道是哪一条有剩余了.

知道哪一条有剩余后, 

**newHead.next = list1 != null || list2 != null? list1 : list2; 即可衔接上链表的剩余部分.**



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
    // 执行用时：1 ms, 在所有 Java 提交中击败了99.64%的用户
    // 内存消耗：38.6 MB, 在所有 Java 提交中击败了93.28%的用户
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        //  将两个链表中的结点按照升序组织成一个链表
        ListNode head = new ListNode(-1);
        ListNode pre = head;
        //  如何让两个链表都遍历完, 短的完了长的可以继续更: 1. 改且
        while(l1!=null && l2!=null) { 
            if (l1.val <= l2.val) {
                pre.next = l1;
                pre = pre.next;
                l1 = l1.next;            
            }
            else {
                pre.next = l2;
                pre = pre.next;
                l2 = l2.next;
            }                                                                       
        }
        //  此时两个链表可能有其中一个已经为空
        //  如果 l1 还有剩余, 追加上剩余的结点
        if (l1 != null) {
            pre.next = l1;      //  连接整条链表            
        }
        //  如果 l2 还有剩余, 追加上剩余的结点
        if (l2 != null) {
            pre.next = l2;
        }
        return head.next;
    }
}
```







