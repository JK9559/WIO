>[84. 柱状图中最大的矩形](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/)
>
>给定 n 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。
>
>求在该柱状图中，能够勾勒出来的矩形的最大面积。
> ![最大矩形面积](https://github.com/JK9559/WIO/blob/master/note/Algorithm/LeetCode/Stack%26Queue/histogram_area.png/)
>
>**示例1：**
```
输入：
  [2,1,5,6,2,3]
输出：
  10
```

```java
// Java版
public class Solution {

    public int largestRectangleArea(int[] heights) {
        if (heights.length <= 0) {
            return 0;
        } else if (heights.length == 1) {
            return heights[0];
        }
        Deque<Integer> stack = new LinkedList<>();
        // 方便计算
        stack.push(-1);
        int res = 0;
        for (int i = 0; i < heights.length; i++) {
            // 如果当前元素 严格小于栈顶元素 说明栈顶元素找到了右边界(又能说明栈内元素的递增的)
            // 所以左右边界齐全 可以计算。
            while (stack.peek() != -1 && heights[i] < heights[stack.peek()]) {
                int cur = stack.pop();
                // 这里是计算 i
                res = Math.max(res, heights[cur] * (i - stack.peek() - 1));
            }
            stack.push(i);
        }
        // 假设遍历完成栈内元素都为递增了，那么就再计算一次
        while (stack.peek() != -1) {
            int cur = stack.pop();
            // 这里是计算 length
            res = Math.max(res, heights[cur] * (heights.length - stack.peek() - 1));
        }
        return res;
    }
}
// 空间复杂度： O(n)
// 时间复杂度： O(n)
```