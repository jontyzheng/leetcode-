#### Question [237. 删除链表中的节点](https://leetcode-cn.com/problems/delete-node-in-a-linked-list/)

tag##



#### Description

请编写一个函数，使其可以删除某个链表中给定的（非末尾）节点。传入函数的唯一参数为 要被删除的节点 。

 

现有一个链表 -- head = [4,5,1,9]，它可以表示为:



 

示例 1：

输入：head = [4,5,1,9], node = 5
输出：[4,1,9]
解释：给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
示例 2：

输入：head = [4,5,1,9], node = 1
输出：[4,5,9]
解释：给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.

提示：

链表至少包含两个节点。
链表中所有节点的值都是唯一的。
给定的节点为非末尾节点并且一定是链表中的一个有效节点。
不要从你的函数中返回任何结果。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/delete-node-in-a-linked-list
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



#### Analysis

###### 1.题目的要求

题目的关键信息是**给定**链表中值为 5 的第二个**节点**.

已知给定的就是原链表中要删除对象的结点的**引用**, 所以要杀要剐都是在给定的结点上做文章.

也难怪题目中之给定一个参数, 没有全局变量原链表的引用, 只有一个参数.



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
    public void deleteNode(ListNode node) {        
        node.val = node.next.val;
        node.next = node.next.next;
        node = node;
    }
}
```





#### 测试用例过滤

无



#### 本期心情						

题目的评论真有意思.

前后强烈的反差.



