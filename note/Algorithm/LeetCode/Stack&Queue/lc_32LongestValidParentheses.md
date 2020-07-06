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
```go
// golang版
func longestValidParentheses(s string) int {
	if len(s) <= 0 {
		return 0
	}
	stack := []int{-1}
	res := 0
	for i := 0; i < len(s); i++ {
		if s[i] == '(' {
			stack = append(stack, i)
		} else {
			stack = stack[:len(stack)-1]
			if len(stack) <= 0 {
				stack = append(stack, i)
			} else {
				// 可以认为在栈里的左括号都是非法的，所以取栈顶元素的下一个位置的左括号作为合法的第一个，求长度就是：i-validBegin+1
				res = maxVali(res, i-(stack[len(stack)-1]+1)+1)
			}
		}
	}
	return res
}

func maxVali(a, b int) int {
	if a > b {
		return a
	} else {
		return b
	}
}
```