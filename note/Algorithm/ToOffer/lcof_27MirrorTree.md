>[剑指 Offer 27. 二叉树的镜像](https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof/)
>
>请完成一个函数，输入一个二叉树，该函数输出它的镜像。
>
>例如输入：
```
     4
   /   \
  2     7
 / \   / \
1   3 6   9
```
>镜像输出：
```
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```
>
>**示例1**
```
输入: 
  root = [4,2,7,1,3,6,9]
输出: 
  [4,7,2,9,6,3,1]
```

```java
// Java 版
public class Solution {

    public TreeNode mirrorTree(TreeNode root) {
        if (root == null) {
            return null;
        } else if (root.left == null && root.right == null) {
            return root;
        } else {
            // 交换树节点
            TreeNode tmp = root.left;
            root.left = root.right;
            root.right = tmp;
            // 递归
            mirrorTree(root.left);
            mirrorTree(root.right);
        }
        return root;
    }
}
```