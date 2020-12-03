#### Question [876. 链表的中间结点](https://leetcode-cn.com/problems/middle-of-the-linked-list/)

效果: 执行用时：0 ms, 在所有 Java 提交中击败了100.00%的用户





#### Description

```
给定一个头结点为 head 的非空单链表，返回链表的中间结点。

如果有两个中间结点，则返回第二个中间结点。

 

示例 1：

输入：[1,2,3,4,5]
输出：此列表中的结点 3 (序列化形式：[3,4,5])
返回的结点值为 3 。 (测评系统对该结点序列化表述是 [3,4,5])。
注意，我们返回了一个 ListNode 类型的对象 ans，这样：
ans.val = 3, ans.next.val = 4, ans.next.next.val = 5, 以及 ans.next.next.next = NULL.
示例 2：

输入：[1,2,3,4,5,6]
输出：此列表中的结点 4 (序列化形式：[4,5,6])
由于该列表有两个中间结点，值分别为 3 和 4，我们返回第二个结点。
 

提示：

给定链表的结点数介于 1 和 100 之间。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/middle-of-the-linked-list
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```



#### Analysis

已知给定的链表结点数是大于 1 的了.

通过草稿可知, 除了 1 以外, 中间结点总是 结点数/2 的位置. 如图

<img src="" width="80%">

所以, 结合另外一道找第 k 个结点的题目可以确定目标结点.

[剑指 Offer 22. 链表中倒数第k个节点](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)



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
    public ListNode middleNode(ListNode head) {
        if (head.next == null)
            return head;
        else
            return findMiddleNode(head);
    }

    public ListNode findMiddleNode(ListNode head) {
        ListNode temp = head;
        int nums = 0;
        while (temp != null) {
            nums++;
            temp = temp.next;
        }

        int position = nums/2;
        int cnt = 1;
        while (cnt <= position) {
            head = head.next;
            cnt++;
        }
        return head;
    }
}
```





#### 测试用例过滤

略



#### 本期发现					

序列的中间位置

只要序列个数不为 1, 奇数偶数的中间结点总是在 len/2 个. (偶数取后面的话)



