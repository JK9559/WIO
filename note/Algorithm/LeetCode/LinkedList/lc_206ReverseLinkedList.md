>[206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)
>
>反转一个单链表。

>**示例：**
```
输入：
  1->2->3->4->5->NULL
```
```
输出：
  5->4->3->2->1->NULL
```

```java
// Java版
// 迭代
class Solution {
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
// 空间复杂度： O(1)
// 时间复杂度： O(n)

// 递归
```