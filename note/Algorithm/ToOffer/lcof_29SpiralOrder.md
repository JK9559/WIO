>[剑指 Offer 29. 顺时针打印矩阵](https://leetcode-cn.com/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/)
>
>输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。
>
>**示例1**
```
输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
输出：[1,2,3,6,9,8,7,4,5]
```

```golang
// Golang 版
func spiralOrder(matrix [][]int) []int {
    if len(matrix) <= 0 || len(matrix[0]) <= 0 {
        return []int{}
    }
    res := []int{}
    r1, r2 := 0, len(matrix)-1
    c1, c2 := 0, len(matrix[0])-1
    for r1 <= r2 && c1 <= c2 {
        for c := c1; c <= c2; c++ {
            res = append(res, matrix[r1][c])
        }
        for r := r1 + 1; r <= r2; r++ {
            res = append(res, matrix[r][c2])
        }
        // 注意这里排除了等于的情况
        if r1 < r2 && c1 < c2 {
            for c := c2 - 1; c > c1; c-- {
                res = append(res, matrix[r2][c])
            }
            for r := r2; r > r1; r-- {
                res = append(res, matrix[r][c1])
            }
        }
        c1++
        c2--
        r1++
        r2--
    }
    return res
}
```