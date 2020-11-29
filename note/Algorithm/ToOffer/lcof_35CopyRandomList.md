>[剑指 Offer 35. 复杂链表的复制](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/)
>
>请实现 ```copyRandomList``` 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 ```next``` 指针指向下一个节点，还有一个 ```random``` 指针指向链表中的任意节点或者 ```null```.
>

```java
// Java 版
public class Solution {
    class Node {
        int val;
        Node next;
        Node random;

        public Node(int val) {
            this.val = val;
            this.next = null;
            this.random = null;
        }
    }
    // 该题因为random指针的存在，无法正常的使用从前到后构建新的链表（因为随机指向无法构造，就算构造了，也不对）
    public Node copyRandomList(Node head) {
        if (null == head) {
            return head;
        }
        Map<Node, Node> dict = new HashMap();
        Node cur = head;
        while (cur != null) {
            // 先保存每个节点对应的新节点
            dict.put(cur, new Node(cur.val));
            cur = cur.next;
        }
        cur = head;
        while (cur != null) {
            // 根据旧链表的关系，重新组装新的链表
            dict.get(cur).next = dict.get(cur.next);
            dict.get(cur).random = dict.get(cur.random);
            cur = cur.next;
        }
        return dict.get(head);
    }
}
```