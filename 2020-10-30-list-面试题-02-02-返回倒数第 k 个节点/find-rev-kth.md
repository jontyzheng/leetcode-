#### Question [面试题 02.02. 返回倒数第 k 个节点](https://leetcode-cn.com/problems/kth-node-from-end-of-list-lcci/)

tag#链表# 



#### Description

```
实现一种算法，找出单向链表中倒数第 k 个节点。返回该节点的值。

注意：本题相对原题稍作改动

示例：

输入： 1->2->3->4->5 和 k = 2
输出： 4
说明：

给定的 k 保证是有效的。

```



#### Analysis

抄的



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
    // 执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户
    // 内存消耗：36.2 MB, 在所有 Java 提交中击败了85.13%的用户
    public int kthToLast(ListNode head, int k) {
        ListNode temp = head;
        int l=1;
        while ((temp = temp.next) != null)
            l++;
        int p = l-k+1;
        while (--p!=0)
            head = head.next;
        return head.val;
    }
}
```



​			





