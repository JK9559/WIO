>[剑指 Offer 32 - II. 从上到下打印二叉树 II](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/)
>
>从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。
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
    [9,20],
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
        queue.offerLast(root);
        // 加入 null 节点 区别是否为下一层
        queue.offerLast(null);
        List<Integer> list = new ArrayList<>();
        while (!queue.isEmpty()) {
            TreeNode node = queue.pollFirst();
            if (node != null) {
                list.add(node.val);
                if (node.left != null) {
                    queue.add(node.left);
                }
                if (node.right != null) {
                    queue.add(node.right);
                }
            } else {
                // 只有当队列内还有值，才放入 null 节点
                if (!queue.isEmpty()) {
                    queue.add(null);
                }
                res.add(list);
                list = new ArrayList<>();
            }
        }
        return res;
    }

}
```