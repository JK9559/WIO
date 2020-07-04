>[92. 反转链表 II](https://leetcode-cn.com/problems/reverse-linked-list-ii/)
>
>反转从位置 m 到 n 的链表。请使用一趟扫描完成反转。
>
>说明:
>1 ≤ m ≤ n ≤ 链表长度。
>**示例：**
```
输入：
  1->2->3->4->5->NULL, m = 2, n = 4
```
```
输出：
  1->4->3->2->5->NULL
```

```java
// Java版
public class Solution {

    public ListNode reverseBetween(ListNode head, int m, int n) {
        if (head == null) {
            return null;
        }
        // prev是待反转头节点的前一个 cur为待反转头
        ListNode prev = null, cur = head;
        while (m > 1) {
            prev = cur;
            cur = cur.next;
            m--;
            n--;
        }
        // 保存待反转的前一个到newHead 记录反转后 反转的链表的为tail
        ListNode newHead = prev, tail = cur;
        while (n > 0) {
            ListNode next = cur.next;

            cur.next = prev;
            prev = cur;
            cur = next;
            n--;
        }
        // 反转后 prev为反转链表的头 cur为反转链表尾的后一个节点 因为 cur = next;
        if (newHead == null) {
            head = prev;
        } else {
            // 连接头
            newHead.next = prev;
        }
        // 连接尾
        tail.next = cur;
        return head;
    }

}
// 空间复杂度： O(1)
// 时间复杂度： O(n)
```