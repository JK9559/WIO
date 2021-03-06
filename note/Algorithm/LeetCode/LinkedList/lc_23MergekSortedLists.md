>[23. 合并K个排序链表](https://leetcode-cn.com/problems/merge-k-sorted-lists/)
>
>合并 k 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。

>**示例：**
```
输入：
  [
    1->4->5,
    1->3->4,
    2->6
  ]
```
```
输出：
  1->1->2->3->4->4->5->6
```
```java
// Java版
public class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        int len = lists.length;
        if (len <= 0) {
            return null;
        } else if (len == 1) {
            return lists[0];
        } else if (len == 2) {
            return mergeTwo(lists[0], lists[1]);
        }
        while (len > 1) {
            // 合并为k路 防止len为奇数
            int k = (len + 1) / 2;
            // 合并多少次
            for (int i = 0; i < len / 2; i++) {
                lists[i] = mergeTwo(lists[i], lists[i + k]);
            }
            len = k;
        }
        return lists[0];
    }

    ListNode mergeTwo(ListNode l1, ListNode l2) {
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
// 空间复杂度 O(logk) 使用了递归
// 时间复杂度：第一轮 合并 k/2 组，每组 O(2n)。第二轮 k/4 组，每组 O(4n)。
// 可得 k/(2^i)*O(2^i * n) +...+ k/2*O(2n) = i的max约为logk
// 综上，时间复杂度为 O(logk * kn)
```