>[24. 两两交换链表中的节点](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)
>
>给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。
>
>**你不能只是单纯的改变节点内部的值**，而是需要实际的进行节点交换。

>**示例：**
```
给定 1->2->3->4, 你应该返回 2->1->4->3.
```

```java
// Java版
class Solution {
    public ListNode swapPairs(ListNode head) {
        if (head == null) {
            return null;
        }
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode p = dummy;
        while (head != null && head.next != null) {
            ListNode first = head;
            ListNode second = head.next;

            p.next = second;
            first.next = second.next;
            second.next = first;

            p = first;
            head = first.next;
        }
        return dummy.next;
    }
}
// 空间复杂度： O(1)
// 时间复杂度： O(n)
```