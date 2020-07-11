>[剑指 Offer 17. 打印从1到最大的n位数](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)
>
>输入数字 ```n``` ，按顺序打印出从 1 到最大的 ```n``` 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。
>
>**示例1**
```
输入：
  n = 1
输出：
  [1,2,3,4,5,6,7,8,9]
```

```java
// Java版 - 快速幂
class Solution {
    public int[] printNumbers(int n) {
        int end = (int)Math.pow(10, n) - 1;
        int[] res = new int[end];
        for(int i = 0; i < end; i++)
            res[i] = i + 1;
        return res;
    }
}
```
```golang
// Golang版
func printNumbers(n int) []int {
    max := int(math.Pow10(n)) - 1
    res := make([]int, max)
    for i := 0; i < max; i++ {
        res[i] = i + 1
    }
    return res
}
```