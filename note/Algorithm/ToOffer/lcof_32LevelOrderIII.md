>[剑指 Offer 32-III. 从上到下打印二叉树 III](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)
>
>请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。
>
>**示例1**
```
给定二叉树: [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
返回：
  [
    [3],
    [20,9],
    [15,7]
  ]
```

```java
// Java 版
public class Solution {

    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) {
            return res;
        }
        Deque<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        queue.add(null);
        // 通过 boolean 实现逆序
        boolean leftToRight = true;
        // 利用 LinkedList 的 addFirst addLast 实现逆序
        LinkedList<Integer> list = new LinkedList<>();
        while (!queue.isEmpty()) {
            TreeNode node = queue.pollFirst();
            if (node != null) {
                if (leftToRight) {
                    list.addLast(node.val);
                } else {
                    list.addFirst(node.val);
                }
                if (node.left != null) {
                    queue.offerLast(node.left);
                }
                if (node.right != null) {
                    queue.offerLast(node.right);
                }
            } else {
                if (!queue.isEmpty()) {
                    queue.offerLast(null);
                }
                // 交换顺序
                leftToRight = !leftToRight;
                res.add(list);
                list = new LinkedList<>();
            }
        }
        return res;
    }

}
```