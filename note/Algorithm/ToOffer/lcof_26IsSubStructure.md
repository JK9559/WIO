>[剑指 Offer 26. 树的子结构](https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/)
>
>输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)
>
>B是A的子结构， 即 A中有出现和B相同的结构和节点值。
>
>例如:
>给定的树 A:
```
     3
    / \
   4   5
  / \
 1   2
```
>给定的树 B：
```
   4 
  /
 1
```
>返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。
>
>**示例1**
```
输入: 
  A = [1,2,3], B = [3,1]
输出: 
  false
```

```java
// Java 版
public class Solution {

    public boolean isSubStructure(TreeNode A, TreeNode B) {
        // 先判断A 是不是完全包含B，如果不是 依次判断A左子树和右子树是不是包含B
        return (A != null && B != null) && (isContain(A, B) || isSubStructure(A.left, B) || isSubStructure(A.right, B));
    }

    /**
     * 判断树A 和 树B 是否是完全包含关系
     *
     * @param A
     * @param B
     * @return
     */
    boolean isContain(TreeNode A, TreeNode B) {
        if (B == null) {
            return true;
        }
        if (A == null || A.val != B.val) {
            return false;
        }
        return isContain(A.left, B.left) && isContain(A.right, B.right);
    }

}
```