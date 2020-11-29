>[剑指 Offer 34. 二叉树中和为某一值的路径](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/)
>
>输入一棵二叉树和一个整数，打印出二叉树中节点值的和为输入整数的所有路径。从树的根节点开始往下一直到叶节点所经过的节点形成一条路径。
>
```
给定二叉树: 
给定如下二叉树，以及目标和 sum = 22，
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
```
```
返回: 
[
   [5,4,11,2],
   [5,8,4,5]
]
```
```java
// Java 版
public class Solution {
    // dfs
    List<List<Integer>> res = new LinkedList<>();
    List<Integer> path = new LinkedList<>();

    public List<List<Integer>> pathSum(TreeNode root, int sum) {
        helper(root, sum);
        return res;
    }

    void helper(TreeNode root, int sum) {
        if (root == null) {
            return;
        }
        sum -= root.val;
        path.add(root.val);
        // 只有为叶子节点并且sum为0的时候，才汇总结果
        if (root.left == null && root.right == null && sum == 0) {
            // 注意这里需要new一个新的path对象
            res.add(new LinkedList<>(path));
        }
        // 递归处理左右子树
        helper(root.left, sum);
        helper(root.right, sum);
        // 剔除不符合条件的元素
        path.remove(path.size() - 1);
    }
}
```