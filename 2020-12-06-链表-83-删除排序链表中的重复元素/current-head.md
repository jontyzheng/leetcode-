#### Question [83. 删除排序链表中的重复元素](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)

tag##



#### Description

```
给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次。

示例 1:

输入: 1->1->2
输出: 1->2
示例 2:

输入: 1->1->2->3->3
输出: 1->2->3

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```



#### Analysis

<img src="" width="80%">



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
    public ListNode deleteDuplicates(ListNode head) {
        if (head == null || head.next == null)
            return head;
        ListNode p = head;
        ListNode q = head.next;
        while (q != null) {
            if (q.val == p.val) {
                q = q.next;         //  下一个结点还是接着下一结点
            }
            else {
                p.next = q;         //  遇到不同的结点才拼接
                p = q;
                q = q.next;
            }
        }
        p.next = q;
        return head;
    }
}
```





#### 测试用例过滤

-



#### 本期发现					

自己不是很懂为什么一开始令 current 指向 head 后, 之后一直是 current 参与运算, 而最后返回 head 就可以得到变化后的整条引用了. head 不是一直未参与运算吗? current 也是另外一个引用而已..

**而 current 指向的是和 head 同一个对象.**(写着写着偶得)



