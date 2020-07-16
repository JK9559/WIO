>[剑指 Offer 31. 栈的压入、弹出序列](https://leetcode-cn.com/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof/)
>
>输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如，序列 {1,2,3,4,5} 是某栈的压栈序列，序列 {4,5,3,2,1} 是该压栈序列对应的一个弹出序列，但 {4,3,5,1,2} 就不可能是该压栈序列的弹出序列。
>
>**示例1**
```
输入：
  pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
输出：
  true
解释：我们可以按以下顺序执行：
push(1), push(2), push(3), push(4), pop() -> 4,
push(5), pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1
```

```java
// Java 版
// 通过模拟栈来实现判断
// 给定一个压入序列 pushed 和弹出序列 popped ，则压入/弹出操作的顺序（即排列）是 唯一确定的
class Solution {
    public boolean validateStackSequences(int[] pushed, int[] popped) {
        Deque<Integer> stack = new LinkedList<>();
        int i = 0;
        for (int num : pushed) {
            // 根据压栈策略压栈
            stack.push(num);
            // 遇到相同元素 则弹栈
            while (!stack.isEmpty() && stack.peek() == popped[i]) {
                stack.pop();
                i++;
            }
        }
        // 当栈最终为空，说明合法
        return stack.isEmpty();
    }
}
```