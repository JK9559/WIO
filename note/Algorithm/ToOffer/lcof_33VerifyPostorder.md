>[剑指 Offer 33. 二叉搜索树的后序遍历序列](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)
>
>输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 true，否则返回 false。假设输入的数组的任意两个数字都互不相同。
>
```
给定二叉树: 
     5
    / \
   2   6
  / \
 1   3
```
```
输入: [1,6,3,2,5]
输出: false
```
```
输入: [1,3,2,6,5]
输出: true
```
```java
// Java 版
public class Solution {

    // 递归
    public boolean verifyPostorder(int[] postorder) {
        return helper(postorder, 0, postorder.length - 1);
    }

    boolean helper(int[] postorder, int begin, int end) {
        if (begin >= end) {
            return true;
        }
        int p = begin;
        // 左子树 < 根
        while (postorder[p] < postorder[end]) {
            p++;
        }
        // m 保存了 右子树的第一个节点
        int m = p;
        // 右子树 > 根
        while (postorder[p] > postorder[end]) {
            p++;
        }
        // 当 p 遍历到末尾了，并且，左子树符合，并且，右子树符合
        return p == end && helper(postorder, begin, m - 1) && helper(postorder, m, end - 1);
    }

}
// 时间复杂度： O(NlogN)《类似快速排序，每次选择一个点，遍历，再分裂 n n-1 n-2 n-4 n-8 求和》 最坏为 链表的情况 O(N^2)
// 空间复杂度：递归空间复杂度为 O(logN) 树深度，最坏为 O(N)
```

```java
public class Solution {
    // 单调栈
    public boolean verifyPostorder(int[] postorder) {
        Deque<Integer> stack = new LinkedList<>();
        // 保存了左子树 父节点的值
        int root = Integer.MAX_VALUE;
        // 逆序遍历数组，说明访问规则为 根 - 右 - 左
        for (int i = postorder.length - 1; i >= 0; i--) {
            // root 应该大于全部左子树节点
            if (postorder[i] > root) {
                return false;
            }
            // 当遇到小于栈顶的元素 根据遍历规则可知，右子树已经遍历完毕，当前为左子树元素，需要找到该元素的父节点
            while (!stack.isEmpty() && postorder[i] < stack.peek()) {
                root = stack.pop();
            }
            stack.push(postorder[i]);
        }
        return true;
    }

}
```