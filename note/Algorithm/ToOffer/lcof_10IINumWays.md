>[剑指 Offer 10- II. 青蛙跳台阶问题](https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/)
>
>一只青蛙一次可以跳上 1 级台阶，也可以跳上 2 级台阶。求该青蛙跳上一个 ```n``` 级的台阶总共有多少种跳法。
>
>答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。
>
>**示例1**
```
输入：
  n = 2
输出：
  2
```
>**示例2**
```
输入：
  n = 7
输出：
  21
```

```java
// Java版
class Solution {
    // 假设跳到n级 为 f(n) 则可以先跳到 f(n-1) 再跳1步 或者 跳到f(n-2) 再跳2步
    // 所以 f(n) = f(n-1) + f(n-2)
    // f(0) = 0 f(1) = 1 f(2) = 2
    public int numWays(int n) {
        if(n==0){
            return 1;
        }
        if (n==1) {
            return 1;
        }
        if (n == 2) {
            return 2;
        }
        int f1 = 1;
        int f2 = 2;
        for(int i=3; i <= n;i++){
            int sum = (f1 + f2) % 1000000007;
            f1 = f2;
            f2 = sum;
        }
        return f2;
    }
}
```