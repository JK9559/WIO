>[剑指 Offer 18. 删除链表的节点](https://leetcode-cn.com/problems/shan-chu-lian-biao-de-jie-dian-lcof/)
>
>给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。返回删除后的链表的头节点。
>
>**示例1**
```
输入：
  head = [4,5,1,9], val = 5
输出：
  [4,1,9]
```

```java
// Java版 - 链表dummy节点
public class Solution {
    public ListNode deleteNode(ListNode head, int val) {
        if (head == null) {
            return null;
        }
        // 使用dummy节点
        ListNode dummy = new ListNode(-1);
        dummy.next = head;
        ListNode prev = dummy;
        while (prev.next != null) {
            if (prev.next.val == val) {
                prev.next = prev.next.next;
                return dummy.next;
            }
            prev = prev.next;
        }
        return dummy.next;
    }
}
```