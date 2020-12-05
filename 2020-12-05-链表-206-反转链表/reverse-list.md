#### Question [206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

tag##



#### Description

```
反转一个单链表。

示例:

输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
进阶:
你可以迭代或递归地反转链表。你能否用两种方法解决这道题？

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/reverse-linked-list
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```



#### Analysis

<img src="https://raw.githubusercontent.com/jontyzheng/leetcode-journal/master/2020-12-05-%E9%93%BE%E8%A1%A8-206-%E5%8F%8D%E8%BD%AC%E9%93%BE%E8%A1%A8/2020-12-05_21-58-32.jpg">



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
    //执行用时：0 ms
    public ListNode reverseList(ListNode head) {
        ListNode precious = null;
        ListNode current = head;
        ListNode nex = null;
        while (current != null) {
            nex = current.next;
            current.next = precious;
            precious = current;
            current = nex;
        }
        return precious;
    }
}
```





#### 测试用例过滤

###### 方案 I

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
        if (head.next == null) {
            return head;
        }   
        else {
            head.next = reverseList(head.next);
        }
        return head;
    }
}
```

用例分析:

```
输入
[1,2,3,4,5]
输出
[1,2,3,4,5]
预期结果
[5,4,3,2,1]
```

解释: 

if 逻辑: 如果给定链表头结点有且只有一个, 返回自己本身, 没有问题.

else 逻辑: 直到遍历到最后一个结点时才开始返回, 前半段没有问题, 刚好走到最后一个节点时, 方法走了 if 的逻辑, 直接返回了 head, 返回原链表.







#### 本期发现					





