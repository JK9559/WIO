>[剑指 Offer 14-II. 剪绳子II](https://leetcode-cn.com/problems/jian-sheng-zi-ii-lcof/)
>
>给你一根长度为 ```n``` 的绳子，请把绳子剪成整数长度的 ```m``` 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 ```k[0],k[1]...k[m-1]``` 。请问 ```k[0]*k[1]*...*k[m-1]``` 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。
>
>答案需要取模 ```1e9+7（1000000007）```，如计算初始结果为：```1000000008```，请返回 ```1```。
>
>**示例1**
```
输入：
  2
输出：
  1
解释：
  2 = 1 + 1, 1 × 1 = 1
```
>**示例2**
```
输入：
  10
输出：
  36
解释：
  10 = 3 + 3 + 4, 3 × 3 × 4 = 36
```

```java
// Java版 数学法+快速幂-推导见lc题解
class Solution {
    public int cuttingRope(int n) {
        if(n <= 3) return n - 1;
        int a = n / 3, b = n % 3;
        if(b == 0) return (int)(qPow(3, a) % 1000000007);
        if(b == 1) return (int)(qPow(3, a - 1) * 4 % 1000000007);
        return (int)(qPow(3, a) * 2 % 1000000007);
    }
    // 快速幂
    long qPow(long x, int n){
        long res = 1;
        while(n > 0){
            if(n%2 == 1){
                res *= x;
                res %= 1000000007;
            }
            x *= x;
            x %= 1000000007;
            n /= 2;
        }
        return res;
    }
}
```