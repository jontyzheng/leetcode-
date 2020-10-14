#### Question [剑指 Offer 52. 两个链表的第一个公共节点](https://leetcode-cn.com/problems/liang-ge-lian-biao-de-di-yi-ge-gong-gong-jie-dian-lcof/)

tag#剑指# #单链表# 



#### Description

------

输入两个链表，找出它们的第一个公共节点。

如下面的两个链表：



在节点 c1 开始相交。

 

示例 1：

![](https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-10-14-list-interview-52-%E4%B8%A4%E4%B8%AA%E9%93%BE%E8%A1%A8%E7%9A%84%E7%AC%AC%E4%B8%80%E4%B8%AA%E5%85%AC%E5%85%B1%E8%8A%82%E7%82%B9/160_statement.png)

输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Reference of the node with value = 8
输入解释：相交节点的值为 8 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。

示例 2：

![](https://github.com/jontyzheng/leetcode-journal/blob/master/2020-10-14-list-interview-52-%E4%B8%A4%E4%B8%AA%E9%93%BE%E8%A1%A8%E7%9A%84%E7%AC%AC%E4%B8%80%E4%B8%AA%E5%85%AC%E5%85%B1%E8%8A%82%E7%82%B9/160_example_2.png)

输入：intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
输出：Reference of the node with value = 2
输入解释：相交节点的值为 2 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [0,9,1,2,4]，链表 B 为 [3,2,4]。在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。

示例 3：

![](https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-10-14-list-interview-52-%E4%B8%A4%E4%B8%AA%E9%93%BE%E8%A1%A8%E7%9A%84%E7%AC%AC%E4%B8%80%E4%B8%AA%E5%85%AC%E5%85%B1%E8%8A%82%E7%82%B9/160_example_2.png)

输入：intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
输出：null
输入解释：从各自的表头开始算起，链表 A 为 [2,6,4]，链表 B 为 [1,5]。由于这两个链表不相交，所以 intersectVal 必须为 0，而 skipA 和 skipB 可以是任意值。
解释：这两个链表不相交，因此返回 null。

注意：

如果两个链表没有交点，返回 null.
在返回结果后，两个链表仍须保持原有的结构。
可假定整个链表结构中没有循环。
程序尽量满足 O(n) 时间复杂度，且仅用 O(1) 内存。
本题与主站 160 题相同：https://leetcode-cn.com/problems/intersection-of-two-linked-lists/

------



#### Analysis

从头往后第一个相交的点相当于从后往前最后一个不相交的点.

不相交可以在 node 之间进行比较. 

从后往前后入栈的先比较可以用栈.

逻辑:

peek 结点, 一旦遍历到相等的结点, peek 后便可 pop 取到 target node.



#### Code

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        // 执行用时：3 ms, 在所有 Java 提交中击败了13.13%的用户
        // 内存消耗：41.8 MB, 在所有 Java 提交中击败了36.07%的用户
        //  node 相等 = next 域和 val 域同时相等
        Stack<ListNode> stack1 = toStack(headA);
        Stack<ListNode> stack2 = toStack(headB);
        ListNode target = null;                  
        while (!stack1.isEmpty() && !stack2.isEmpty()) {
            ListNode nodeA = stack1.peek();
            ListNode nodeB = stack2.peek();
            if (nodeA != nodeB) {   
                break;
            }
            //  如果peak到当前结点不相等, 就break跳出
            //  遍历到相等的 node 时赋值跳出
            else {
                target = stack1.pop();
                stack2.pop();                
            }            
        }
        return target;
    }

    public Stack<ListNode> toStack(ListNode head) {
        Stack<ListNode> list = new Stack<>();
        while (head != null) {
            list.push(head);
            head = head.next;
        }
        return list;
    }
}
        
```







