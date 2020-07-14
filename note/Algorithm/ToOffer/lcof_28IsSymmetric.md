>[剑指 Offer 28. 对称的二叉树](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/)
>
>请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。
>
>例如，二叉树 [1,2,2,3,4,4,3] 是对称的。
>
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```
>但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:
```
    1
   / \
  2   2
   \   \
   3    3
```
>
>**示例1**
```
输入: 
  root = [1,2,2,3,4,4,3]
输出: 
  true
```

```java
// Java 版
class Solution {
    public boolean isSymmetric(TreeNode root) {
        // 当根为null 或者 左右子树对称
        return root == null || resolve(root.left, root.right);
    }

    boolean resolve(TreeNode left, TreeNode right) {
        // 左右子树都为null说明对称
        if (left == null && right == null) {
            return true;
        }
        // 其中一个不为null 或者 数值不同 不对称
        if (left == null || right == null || left.val != right.val) {
            return false;
        }
        // 继续判断两个树的四个孩子，是否你的左等于我的右，你的右等于我的左
        return resolve(left.left, right.right) && resolve(left.right, right.left);
    }
}
```