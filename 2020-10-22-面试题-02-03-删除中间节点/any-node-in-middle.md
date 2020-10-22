#### Question [面试题 02.03. 删除中间节点](https://leetcode-cn.com/problems/delete-middle-node-lcci/)

tag#单链表# 



#### Description

```
实现一种算法，删除单向链表中间的某个节点（即不是第一个或最后一个节点），假定你只能访问该节点。

 

示例：

输入：单向链表a->b->c->d->e->f中的节点c
结果：不返回任何数据，但该链表变为a->b->d->e->f

```



#### Analysis

切换到英文版本看题就会很容易看懂题目要求

> delete a node in the middle (i.e., any node but the first and last node, not necessarily the exact middle) of a singly linked list
>
> ------
>
> 删除中间位置的结点, 只要不是第一个和最后一个
>
> 也不一定就要正中间的结点





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
    // 内存消耗：37.9 MB, 在所有 Java 提交中击败了93.58%的用户
    public void deleteNode(ListNode node) {
          node.val = node.next.val;
          node.next = node.next.next;      
    }
}
```





