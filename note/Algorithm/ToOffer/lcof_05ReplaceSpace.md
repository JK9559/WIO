>[剑指 Offer 05. 替换空格](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)
>
>请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

>**示例：**
```
输入：
  s = "We are happy."
输出：
  "We%20are%20happy."
```

```java
// Java版
public class Solution {

    public String replaceSpace(String s) {
        if (s.length() <= 0) {
            return s;
        }
        // 这里需要申请三倍的char数组
        char[] newStr = new char[3 * s.length()];
        int size = 0;
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == ' ') {
                newStr[size] = '%';
                size++;
                newStr[size] = '2';
                size++;
                newStr[size] = '0';
                size++;
            } else {
                newStr[size] = s.charAt(i);
                size++;
            }
        }
        // 这里是 char数组 转String
        return new String(newStr, 0, size);
    }

}
// 空间复杂度： O(n)
// 时间复杂度： O(n) 字符串的长度
```
```go
// golang版
func replaceSpace(s string) string {
    if len(s) <= 0 {
        return s
    }
    blank := []byte{' ', ' '}
    oldStr := []byte(s)
    newStr := []byte(s)
    for i := 0; i < len(s); i++ {
        if oldStr[i] == ' ' {
            newStr = append(newStr, blank...)
        }
    }
    oldTail, newTail := len(oldStr)-1, len(newStr)-1
    for oldTail != newTail {
        if oldStr[oldTail] == ' ' {
            newStr[newTail] = '0'
            newTail--
            newStr[newTail] = '2'
            newTail--
            newStr[newTail] = '%'
            newTail--
        } else {
            newStr[newTail] = oldStr[oldTail]
            newTail--
        }
        oldTail--
    }
    return string(newStr)
}
```