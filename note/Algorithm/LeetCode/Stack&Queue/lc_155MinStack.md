>[155. 最小栈](https://leetcode-cn.com/problems/min-stack/)
>
>设计一个支持 push ，pop ，top 操作，并能在常数时间内检索到最小元素的栈。
>
> * push(x) —— 将元素 x 推入栈中。
> * pop() —— 删除栈顶的元素。
> * top() —— 获取栈顶元素。
> * getMin() —— 检索栈中的最小元素。
>
>**示例1：**
```
输入：
  ["MinStack","push","push","push","getMin","pop","top","getMin"]
  [[],[-2],[0],[-3],[],[],[],[]]
输出：
  [null,null,null,null,-3,null,0,-2]
解释：
  MinStack minStack = new MinStack();
  minStack.push(-2);
  minStack.push(0);
  minStack.push(-3);
  minStack.getMin();   --> 返回 -3.
  minStack.pop();
  minStack.top();      --> 返回 0.
  minStack.getMin();   --> 返回 -2.
```
>**示例2：**
```
输入：
  "([)]"
输出：
  false
```

```java
// Java版
public class Solution {

    class MinStack {

        Deque<Integer> stack;
        Deque<Integer> minStack;

        /**
         * initialize your data structure here.
         */
        public MinStack() {
            stack = new LinkedList<>();
            minStack = new LinkedList<>();
        }

        public void push(int x) {
            stack.push(x);
            if (minStack.size() <= 0) {
                minStack.push(x);
            } else {
                int top = minStack.peek();
                minStack.push(Math.min(top, x));
            }
        }

        public void pop() {
            stack.pop();
            minStack.pop();
        }

        public int top() {
            if (stack.size() <= 0) {
                return -1;
            }
            return stack.peek();
        }

        public int getMin() {
            if (minStack.size() <= 0) {
                return -1;
            }
            return minStack.peek();
        }
    }

}
```