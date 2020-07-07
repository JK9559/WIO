>[剑指 Offer 07. 重建二叉树](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/)
>
>输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。
>
>例如，给出
```
  前序遍历 preorder = [3,9,20,15,7]
  中序遍历 inorder = [9,3,15,20,7]
```
```
  返回如下二叉树：
    3
   / \
  9  20
    /  \
   15   7  
```

```java
// Java版
class Solution {
    // 使用hashmap做中序节点的缓存
    Map<Integer, Integer> inorderMap;
    int[] preorder;

    public TreeNode buildTree(int[] preorder, int[] inorder) {
        if (preorder.length <= 0) {
            return null;
        }
        inorderMap = new HashMap<>(inorder.length);
        for (int i = 0; i < inorder.length; i++) {
            inorderMap.put(inorder[i], i);
        }
        this.preorder = preorder;
        return build(0, preorder.length - 1, 0, inorder.length - 1);
    }

    TreeNode build(int preL, int preR, int inL, int inR) {
        if (preL > preR || inL > inR) {
            return null;
        }
        TreeNode root = new TreeNode(preorder[preL]);
        int idx = inorderMap.get(preorder[preL]);
        // 重点在划分节点
        root.left = build(preL + 1, preL + idx - inL, inL, inL + idx - 1 - inL);
        root.right = build(preL + idx - inL + 1, preR, idx + 1, inR);
        return root;
    }
}
// 空间复杂度： O(n)
// 时间复杂度： O(n) 链表长度
```
```go
// golang版
// 非递归版，需要仔细理解
func buildTree(preorder []int, inorder []int) *TreeNode {
    if len(preorder) <= 0 {
        return nil
    }
    root := &TreeNode{}
    root.Val = preorder[0]
    stack := []*TreeNode{root}
    inorderInd := 0
    for i := 1; i < len(preorder); i++ {
        node := stack[len(stack)-1]
        preVal := preorder[i]
        // 比如简单的树 可以看到：
        // 如果中序的第一个节点不是根 那么就说明 当前这个前序是左子树
        // 否则为右子树
        if node.Val != inorder[inorderInd] {
            node.Left = &TreeNode{}
            node.Left.Val = preVal
            stack = append(stack, node.Left)
        } else {
            // 前序的下一个元素的右子树的，需要找是哪个节点的右子树。
            // 通过中序 可以从前向后遍历，前序需要从后向前遍历，找到最后一次相等的值 就是当前这个元素的父节点。
            // 因此 需要倒序遍历已经遍历的节点用栈
            for len(stack) > 0 && stack[len(stack)-1].Val == inorder[inorderInd] {
                node = stack[len(stack)-1]
                stack = stack[:len(stack)-1]
                inorderInd++
            }
            node.Right = &TreeNode{}
            node.Right.Val = preVal
            stack = append(stack, node.Right)
        }
    }
    return root
}
```