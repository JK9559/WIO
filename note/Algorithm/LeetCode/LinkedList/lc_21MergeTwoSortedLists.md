>[21. 合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)
>
>将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 
>
>**示例：**
```
输入：1->2->4, 1->3->4
```
```
输出：1->1->2->3->4->4
```
```java
// Java版
public class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        if (l1 == null) {
            return l2;
        } else if (l2 == null) {
            return l1;
        }
        ListNode dummy = new ListNode(-1);
        ListNode p = dummy;
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                p.next = l1;
                l1 = l1.next;
            } else {
                p.next = l2;
                l2 = l2.next;
            }
            p = p.next;
        }
        if (l1 == null) {
            p.next = l2;
        }
        if (l2 == null) {
            p.next = l1;
        }
        return dummy.next;
    }
}
// 时间复杂度 O(m+n) 空间复杂度 O(1)
```
```go
// golang版
func mergeTwoLists(l1 *ListNode, l2 *ListNode) *ListNode {
    if l1 == nil {
        return l2
    }
    if l2 == nil {
        return l1
    }
    dummy := &ListNode{}
    p := dummy
    for l1 != nil && l2 != nil {
        if l1.Val < l2.Val {
            p.Next = l1
            l1 = l1.Next
        }else{
            p.Next = l2
            l2 = l2.Next
        }
        p = p.Next
    }
    if l1 == nil {
        p.Next = l2
    }
    if l2 == nil {
        p.Next = l1
    }
    return dummy.Next
}
```