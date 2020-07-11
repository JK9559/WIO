>[剑指 Offer 16. 数值的整数次方](https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/)
>
>实现函数 ```double Power(double base, int exponent)```，求 ```base``` 的 ```exponent``` 次方。不得使用库函数，同时不需要考虑大数问题。
>
>**示例1**
```
输入：
  2.00000, 10
输出：
  1024.00000
```

```java
// Java版 - 快速幂
class Solution {
    /**
     * 快速幂
     * 求 x^77:
     * 	77的二进制为1001101
     * 	所以
     * 	x^77 = x^64 * x^8 * x^4 * x^1 也就是说 遇到1 res就乘一个数如下代码
     */
    public double myPow(double x, int n) {
        if(x == 0) return 0;
        // 防止溢出 定义为long
        long b = n;
        double res = 1.0;
        if(b < 0) {
            x = 1 / x;
            b = -b;
        }
        while(b > 0) {
            if((b & 1) == 1) res *= x;
            x *= x;
            b >>= 1;
        }
        return res;
    }
}
```