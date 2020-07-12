>[剑指 Offer 24. 反转链表](https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/)
>
>定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。
>
>**示例1**
```
输入: 
  1->2->3->4->5->NULL
输出: 
  5->4->3->2->1->NULL
```

```java
// Java 版
public class Solution {

    public ListNode reverseList(ListNode head) {
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
```

```golang
// Golang版
func reverseList(head *ListNode) *ListNode {
    if head == nil {
        return head
    }
    var prev *ListNode
    for head != nil {
        next := head.Next

        head.Next = prev
        prev = head
        head = next
    }
    return prev
}
```