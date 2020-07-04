>[32. 最长有效括号](https://leetcode-cn.com/problems/longest-valid-parentheses/)
>
>给定一个只包含 '(' 和 ')' 的字符串，找出最长的包含有效括号的子串的长度。
>
>**示例1：**
```
输入：
  "(()"
输出：
  2
解释：
  最长有效括号子串为 "()"
```
>**示例2：**
```
输入：
  ")()())"
输出：
  4
解释：
  最长有效括号子串为 "()()"
```

```java
// Java版
public class Solution {
    
    public int longestValidParentheses(String s) {
        if (s.length() <= 0) {
            return 0;
        }
        // 栈中存：当前还非法的字符的下标
        Deque<Integer> stack = new LinkedList<>();
        stack.push(-1);
        int res = 0;
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                stack.push(i);
            } else {
                stack.pop();
                if (stack.size() <= 0) {
                    stack.push(i);
                } else {
                    // 计算长度时 计算从当前非法的下一位(栈顶+1)到当前元素的元素位数
                    res = Math.max(res, i - (stack.peek() + 1) + 1);
                }
            }
        }
        return res;
    }
}
// 空间复杂度： O(n)
// 时间复杂度： O(n)
```
```java
// dp
```