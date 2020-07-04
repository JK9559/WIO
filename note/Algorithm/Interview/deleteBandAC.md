>删除连续ac和b
>
>字符串包含小写字母，删除连续的ac和b。 
>
>**示例：**
```
输入：abc
```
```
输出：""
```
```java
// Java版
public class Solution {

    public static String delBAndAC(String str) {
        if (str.length() <= 0) {
            return str;
        }
        char[] chars = str.toCharArray();
        // 栈保存留下的字母
        Deque<Character> stack = new LinkedList<>();
        for (char ch : chars) {
            // 遇到b不入栈
            if (ch == 'b') {
                continue;
                // 遇到c取栈顶 如果为a则弹栈，否则入栈
            } else if (ch == 'c') {
                if (stack.size() > 0 && stack.peek() == 'a') {
                    stack.pop();
                } else {
                    stack.push(ch);
                }
            } else {
                // 其他字母都入栈
                stack.push(ch);
            }
        }
        int len = stack.size();
        char[] res = new char[len];
        for (int i = len - 1; i >= 0; i--) {
            res[i] = stack.pop();
        }
        return new String(res);
    }

    public static void main(String[] args) {
        System.out.println(delBAndAC("aabcc"));
        System.out.println(delBAndAC("bbdfg"));
        System.out.println(delBAndAC("bb"));
        System.out.println(delBAndAC("ac"));
        System.out.println(delBAndAC("aaac"));
        System.out.println(delBAndAC("c"));
        System.out.println(delBAndAC("abc"));
    }
}
// 时间复杂度 O(n) 空间复杂度 O(n)
```