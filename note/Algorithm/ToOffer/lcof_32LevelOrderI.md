>[剑指 Offer 32-I. 从上到下打印二叉树](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/)
>
>从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。
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
  [3,9,20,15,7]
```

```java
// Java 版
public class Solution {

    public int[] levelOrder(TreeNode root) {
        // 特判当树为空
        if (root == null) {
            return new int[0];
        }
        // 用队列实现BFS
        Deque<TreeNode> queue = new LinkedList<>();
        // 先push根节点
        queue.offerLast(root);
        List<Integer> res = new ArrayList<>();
        while (!queue.isEmpty()) {
            TreeNode node = queue.pollFirst();
            res.add(node.val);
            if (node.left != null) {
                queue.offerLast(node.left);
            }
            if (node.right != null) {
                queue.offerLast(node.right);
            }
        }
        int[] result = new int[res.size()];
        for (int i = 0; i < res.size(); i++) {
            result[i] = res.get(i);
        }
        return result;
    }

}
```