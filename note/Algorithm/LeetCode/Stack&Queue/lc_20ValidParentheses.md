>[20. 有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)
>
>给定一个只包括 '('，')'，'{'，'}'，'['，']' 的字符串，判断字符串是否有效。
>
>有效字符串需满足：
>
> * 左括号必须用相同类型的右括号闭合。
> * 左括号必须以正确的顺序闭合。
> * 注意空字符串可被认为是有效字符串。
>
>**示例1：**
```
输入：
  "()[]{}"
输出：
  true
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
class Solution {
    public boolean isValid(String s) {
        if (s.length() <= 0) {
            return true;
        }
        // 使用hashmap缓存匹配规则
        HashMap<Character, Character> map = new HashMap<>();
        map.put('(', ')');
        map.put('[', ']');
        map.put('{', '}');
        Deque<Character> stack = new LinkedList<>();
        for (char ch : s.toCharArray()) {
            if (ch == '(' || ch == '[' || ch == '{') {
                stack.push(ch);
            } else {
                if (stack.size() > 0 && map.get(stack.peek()) == ch) {
                    stack.pop();
                } else {
                    return false;
                }
            }
        }
        // 最终必须全部匹配 才算成功
        return stack.size() == 0;
    }
}
// 空间复杂度： O(n)
// 时间复杂度： O(n)
```