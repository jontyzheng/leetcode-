#### Question [234. 回文链表](https://leetcode-cn.com/problems/palindrome-linked-list/)

tag##



#### Description

```
请判断一个链表是否为回文链表。

示例 1:

输入: 1->2
输出: false
示例 2:

输入: 1->2->2->1
输出: true
进阶：
你能否用 O(n) 时间复杂度和 O(1) 空间复杂度解决此题？

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/palindrome-linked-list
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```



#### Analysis

一个链表是否回文实际上问的是它各个结点的数值是否回文.

而回文序列的特点就是两边镜面对称.



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
    //执行用时：4 ms, 在所有 Java 提交中击败了31.57%
    public boolean isPalindrome(ListNode head) {
        List<ListNode> list = new ArrayList<>();
        boolean isPalindrome = true;
        if (head == null)
            return true;                 
        while (head != null) {
            list.add(head);
            head = head.next;
        }
        for (int i = 0, j = list.size()-1; i < j; i++, j--) {
            if ( list.get(i).val != list.get(j).val ) {
                isPalindrome = false;
                break;
            }
        }
        return isPalindrome;
    }
}
```





#### 测试用例过滤

I.偷梁换柱, 将链表各个结点的值用 ArrayList 装起来, 然后当成数组判断.

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
    public boolean isPalindrome(ListNode head) {
        List<Integer> list = new ArrayList<>();
        boolean isPalindrome = true;
        while (head != null) {
            list.add(head.val);
            head = head.next;
        }
        for (int i = 0, j = list.size()-1; i < j; i++, j--) {
            if (list.get(i) != list.get(j)) {
                isPalindrome = false;
                break;
            }
        }
        return isPalindrome;
    }
}
```

> **24 / 26** 个通过测试用例
>
> ```
> 输入：
> [-129,-129]
> 输出：
> false
> 预期：
> true
> ```

原因: 从 List<Interger> 的列表中取出 127 以内的值会封装成值返回数值本身, 但以外的数值就会返回其对象.

可以将 == 换成 equals 方法.

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
    //执行用时: 4 ms
    public boolean isPalindrome(ListNode head) {
        List<Integer> list = new ArrayList<>();
        boolean isPalindrome = true;
        if (head == null)
            return true;                 
        while (head != null) {
            list.add(head.val);
            head = head.next;
        }
        for (int i = 0, j = list.size()-1; i < j; i++, j--) {
            if ( !list.get(i).equals(list.get(j)) ) {
                isPalindrome = false;
                break;
            }
        }
        return isPalindrome;
    }
}
```





或者, 存 node, 然后拿 node 的 val 出来比较.

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
    //执行用时：4 ms, 在所有 Java 提交中击败了31.57%
    public boolean isPalindrome(ListNode head) {
        List<ListNode> list = new ArrayList<>();
        boolean isPalindrome = true;
        if (head == null)
            return true;                 
        while (head != null) {
            list.add(head);			/*update: add(node.val) - add(node)*/
            head = head.next;
        }
        for (int i = 0, j = list.size()-1; i < j; i++, j--) {
            if ( list.get(i).val != list.get(j).val ) {
                /*update: get(i) != get(j) - get(i).val != get(j).val*/
                isPalindrome = false;	
                break;
            }
        }
        return isPalindrome;
    }
}
```





#### 本期心情						

判断链表一个是否回文的依据是数值是否回文.

而回文的特点一定是两边对照相等的.

就是, 还知道了 集合类中存储 Integer 的隐藏特点. 127



