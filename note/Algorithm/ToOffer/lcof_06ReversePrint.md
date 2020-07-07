>[剑指 Offer 06. 从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)
>
>输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

>**示例：**
```
输入：
  head = [1,3,2]
输出：
  [2,3,1]
```

```java
// Java版
class Solution {
    public int[] reversePrint(ListNode head) {
        if (head == null) {
            return new int[0];
        }
        Deque<Integer> stack = new LinkedList<>();
        while (head != null) {
            stack.push(head.val);
            head = head.next;
        }
        int size = stack.size();
        int[] res = new int[size];
        for (int i = 0; i < res.length; i++) {
            res[i] = stack.pop();
        }
        return res;
    }
}
// 空间复杂度： O(n)
// 时间复杂度： O(n) 链表长度
```
```go
// golang版
func reversePrint(head *ListNode) []int {
    if head == nil {
        return []int{}
    }
    stack := []int{}
    for head != nil {
        stack = append(stack, head.Val)
        head = head.Next
    }
    l, r := 0, len(stack)-1
    // 注意原地交换
    for l < r {
        stack[l], stack[r] = stack[r], stack[l]
        l++
        r--
    }
    return stack
}
```