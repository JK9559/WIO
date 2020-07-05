>[72. 编辑距离](https://leetcode-cn.com/problems/edit-distance/)
>
> 给你两个单词 word1 和 word2，请你计算出将 word1 转换成 word2 所使用的最少操作数 。
>
>你可以对一个单词进行如下三种操作：
>
> * 插入一个字符
> * 删除一个字符
> * 替换一个字符
>
>*示例1：*
```
输入：
  word1 = "horse", word2 = "ros"
输出：
  3
解释：
  horse -> rorse (将 'h' 替换为 'r')
  rorse -> rose (删除 'r')
  rose -> ros (删除 'e')
```
>*示例2：*
```
输入：
  word1 = "intention", word2 = "execution"
输出：
  5
解释：
  intention -> inention (删除 't')
  inention -> enention (将 'i' 替换为 'e')
  enention -> exention (将 'n' 替换为 'x')
  exention -> exection (将 'n' 替换为 'c')
  exection -> execution (插入 'u')
```

```java
// Java版
public class Solution {

    public int minDistance(String word1, String word2) {
        int len1 = word1.length();
        int len2 = word2.length();
        // 注意遍历的时候 处理 <= len1 <= len2
        int[][] dp = new int[len1 + 1][len2 + 1];
        // 当word1为空，转换为word2 需要的步数为 dp[0][i] 需要每次对word1增加一个字母
        for (int i = 1; i <= len2; i++) {
            dp[0][i] = dp[0][i - 1] + 1;
        }
        // 当word2为空，word1转换为word2 需要的步数为 dp[i][0] 需要每次对word1减少一个字母
        for (int i = 1; i <= len1; i++) {
            dp[i][0] = dp[i - 1][0] + 1;
        }
        // 当word1 和 word2 都不为空 需要的步数为 dp[len1][len2]
        for (int i = 1; i <= len1; i++) {
            for (int j = 1; j <= len2; j++) {
                // 如果当前两个字母相同，结果等于同时去掉这两个字母的情况。否则有三种情况
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    // 否则，按照word1到word2的变换规则，有三种情况
                    // 1. word1新增一个字母 变到word2 --> dp[i][j-1] --> word1先匹配word2前部 最后再在word1后增加一个word2的尾字母
                    // 2. word1删除一个字母 变到word2 --> dp[i-1][j] --> word1去掉最后一位匹配到word2 最后去掉word1的尾字母
                    // 3. word1变换一个字母 变到word2 --> dp[i-1][j-1] --> 两单词前部匹配，然后word1的尾字母变换为word2的尾字母
                    dp[i][j] = Math.min(dp[i][j - 1], Math.min(dp[i - 1][j - 1], dp[i - 1][j])) + 1;
                }
            }
        }
        return dp[len1][len2];
    }
    
}
// 空间复杂度： O(mn) m n分别为word1 word2的长度
// 时间复杂度： O(mn)
```
```golang
// golang版
func minDistance(word1 string, word2 string) int {
	n1, n2 := len(word1), len(word2)
	// dp[i][j] 代表word1 1-i 变换到 word2 1-j 需要几步
	dp := make([][]int, n1+1)
	for i := 0; i <= n1; i++ {
		dp[i] = make([]int, n2+1)
	}
	// 当word1为空 变到 word2 每一步需要添加1个字母 所以+1
	for i := 1; i <= n2; i++ {
		dp[0][i] = dp[0][i-1] + 1
	}
	// 当word2为空 word1 变到word2 每一步需要删除一个字母 所以操作次数+1
	for i := 1; i <= n1; i++ {
		dp[i][0] = dp[i-1][0] + 1
	}
	for i := 1; i <= n1; i++ {
		for j := 1; j <= n2; j++ {
			if word1[i-1] == word2[j-1] {
				// 从1开始 当word1 第i 等于word2 第j
				// 说明只需要知道i前面 和j前面的单词经过多少就行
				dp[i][j] = dp[i-1][j-1]
			} else {
				// 求dp[i][j] 有三种变换：
				// 以 word1 为 "horse"，word2 为 "ros"，且 dp[5][3] 为例，即要将 word1的前 5 个字符转换为 word2的前 3 个字符，也就是将 horse 转换为 ros，因此有：
				//(1) dp[i-1][j-1]，即先将 word1 的前 4 个字符 hors 转换为 word2 的前 2 个字符 ro，然后将第五个字符 word1[4]（因为下标基数以 0 开始） 由 e 替换为 s（即替换为 word2 的第三个字符，word2[2]）
				//(2) dp[i][j-1]，即先将 word1 的前 5 个字符 horse 转换为 word2 的前 2 个字符 ro，然后在末尾补充一个 s，即插入操作
				//(3) dp[i-1][j]，即先将 word1 的前 4 个字符 hors 转换为 word2 的前 3 个字符 ros，然后删除 word1 的第 5 个字符
				dp[i][j] = minTrans(dp[i-1][j-1], minTrans(dp[i-1][j], dp[i][j-1])) + 1
			}
		}
	}
	return dp[n1][n2]
}

func minTrans(a, b int) int {
	if a < b {
		return a
	} else {
		return b
	}
}
```