#### Question [剑指 Offer 06. 从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

tag#剑指 offer# #链表#



#### Description

```
输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

 

示例 1：

输入：head = [1,3,2]
输出：[2,3,1]
 

限制：

0 <= 链表长度 <= 10000
```



#### Analysis

按照链表的思路走即可 加上 ArrayList.get(i) 的 API 



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
    public int[] reversePrint(ListNode head) {
        // 执行用时：1 ms, 在所有 Java 提交中击败了73.18%的用户
        // 内存消耗：39.4 MB, 在所有 Java 提交中击败了72.13%的用户
        List<Integer> list = new ArrayList<>();
        while (head != null) {
            int x = head.val;
            list.add(x);
            head = head.next;
        }
        int[] target = new int[list.size()];
        int j=0;
        for (int i=target.length-1; i>=0; i--) {
            target[j] = list.get(i);
            j++;
        }
        return target;
    }
}
```







