#### Question [203. 移除链表元素](https://leetcode-cn.com/problems/remove-linked-list-elements/)

tag##



#### Description

```
删除链表中等于给定值 val 的所有节点。

示例:

输入: 1->2->6->3->4->5->6, val = 6
输出: 1->2->3->4->5
```





#### Analysis

###### I. 问题

移除其中, **所有** 值匹配的结点

###### II. 说明什么

说明每次都要匹配删除拼接

###### III. 好的方法

从当前结点开始, 每次判断下一个结点的数值域有没有和 val 匹配, 若匹配, 就让当前结点的下一个结点域指向下一个结点的 next.

否, 就更新当前结点.

###### V. 有没有需要注意的地方

因为, 这样的下去 current 会跟着遍历而跑掉. 所以最好一开始有一条线牵着 current.

新建一个全空的结点, 随意假设一个无意义的值构造. 让它的下一个指针域牵着 current.



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
    //执行用时：1 ms
    public ListNode removeElements(ListNode head, int val) {
                    
        ListNode freshNode = new ListNode(-1);
        ListNode current = head; 
        freshNode.next = current;   //  等同于 freshNode.next = head
        current = freshNode;        //  偷梁换柱, 每次都保证了current的当前结点总是有值 每次从 next 问起

        while (current.next != null) {   
            //  update: ∵确定当前的current从-1开始, 所以每次都可以大胆地对下一个值实际也是原链表中的结点
            if ( current.next != null && current.next.val == val) {                
                current.next = current.next.next;                
            }
            else {                              
                current = current.next;                
            }            
        }        
        return freshNode.next;
    }
}
```





#### 测试用例过滤

略



#### 本期发现					

链表结点的删除每次从下一个指针开始判断也不错. 每次更新都是当前结点直接将下一个结点的下一个结点域更新为当前结点的下一个结点域.

通过设置一个无意义的空结点可以起到"牵线"的作用.



