#### Question [面试题 02.06. 回文链表](https://leetcode-cn.com/problems/palindrome-linked-list-lcci/)

tag#链表# #反转# #是否回文#



#### Description



#### Analysis

和字符串的回文, 数组的回文本质上是一样的. 就同一个序列两端比较.

先将链表的 val 取下来放到一个序列中. 

借助数组的思路, 从起点遍历到终点 size/2.

每次当前的 i 和 size - 1 - i 个值匹配. 当匹配到不相等的, 直接返回 false 结束程序.

假如循环完整进行下来了, 中间没有结束, 那就可以确定序列的两端都两两相等了. 可返回 true 了.



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
    //执行用时：4 ms, 在所有 Java 提交中击败了22.70%的用户
    //内存消耗：42.4 MB, 在所有 Java 提交中击败了28.55%的用户
    public boolean isPalindrome(ListNode head) {
        List<Integer> nodes = new ArrayList<>();
        ListNode node = head;
        while (node != null) {
            nodes.add(node.val);
            node = node.next;
        }
        //  得到链表中 val 值链表
        int size = nodes.size();                
        for (int l = 0; l < size / 2; l++) {
            int left = nodes.get(l);
            int right = nodes.get(size - l - 1);
            if (left != right)
                return false;
        }
        return true;
    }
}
```





#### 结论			

一个序列的回文比较.

第 i 个数据一定和 第 size - 1- i 个数据相等. (其中, i < size/2).





