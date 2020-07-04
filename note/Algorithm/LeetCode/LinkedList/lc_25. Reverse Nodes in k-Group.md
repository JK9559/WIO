>[25. K 个一组翻转链表](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/)
>
>给你一个链表，每 k 个节点一组进行翻转，请你返回翻转后的链表。
>
>k 是一个正整数，它的值小于或等于链表的长度。
>
>如果节点总数不是 k 的整数倍，那么请将最后剩余的节点保持原有顺序。

>**示例：**
```
给你这个链表：1->2->3->4->5
当 k = 2 时，应当返回: 2->1->4->3->5
当 k = 3 时，应当返回: 3->2->1->4->5
```

```java
// Java版
public class Solution {

    public ListNode reverseKGroup(ListNode head, int k) {
        if (head == null) {
            return null;
        }
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        // begin end 指向待反转的前一个节点
        ListNode begin = dummy, end = dummy;
        while (end.next != null) {
            for (int i = 0; end != null && i < k; i++) {
                end = end.next;
            }
            // end指向待反转的最后一个位置
            if (end == null) {
                break;
            }
            // start 为待反转的头结点
            ListNode start = begin.next;
            // next 保存反转后链表尾节点的next
            ListNode next = end.next;
            // 为了方便反转
            end.next = null;
            // 反转并连接头结点
            begin.next = reverse(start);
            // 反转后 start为链表尾节点
            // 插入知识点：reverse函数传值 没传引用 如果传了引用 start会变为null
            // 也就是反转后链表尾节点的next
            // 这里的start还是上面赋值的值 也就是反转后链表的尾节点
            start.next = next;
            begin = start;
            end = start;
        }
        return dummy.next;
    }

    ListNode reverse(ListNode head) {
        if (head == null) {
            return null;
        }
        ListNode prev = null;
        while (head != null) {
            ListNode next = head.next;

            head.next = prev;
            prev = head;
            head = next;
        }
        return prev;
    }
}
// 空间复杂度： O(1)
// 时间复杂度： O(n)
```